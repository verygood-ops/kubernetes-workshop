# Kubernetes Jobs

Lets say we have some directory where video files appears. They will be our queue. We need to convert this files to some basic resolutions.\
In real life it is tipical job for video streaming services like YouTube.com 

## Simple Job

Create a directory that will be filled by files.\
All commands below are related to macOS. 
```bash
mkdir /Users/$USER/queue-files
```
Download sample video files. They will be our queue.
Change `USERNAME` with your login name.
```bash
wget http://www.jell.yfish.us/media/jellyfish-{3,5,10}-mbps-hd-h264.mkv -P /Users/USERNAME/queue-files/
```

Use a file [job-ffmpeg.yaml](job-ffmpeg.yaml) with a job to deal with our "queue". Change `USERNAME` with your login name.

Run the job.
 
```
 kubectl create -f job-ffmpeg.yaml
```
And watch the status.
```
kubectl describe jobs/converter
```

To see results of job execution, run

```bash
pods=$(kubectl get pods --selector=job-name=converter --output=jsonpath={.items..metadata.name}); kubectl logs $pods
```
You should see ffmpeg output

To clean pods not needed anymore run
```
kubectl delete -f job-ffmpeg.yaml
```

## Cron jobs

Suppose we need to convert files only from time to time. So our job need to be a cron job!
[job-cron-ffmpeg.yaml](job-cron-ffmpeg.yaml) will do the trick

Check cronjobs with\
```
kubectl get cronjobs
```

```
NAME      SCHEDULE      SUSPEND   ACTIVE    LAST SCHEDULE   AGE
converter   */1 * * * *   False     0         13s             1m
```

Delete cronjob\
```
kubectl delete -f ./job-cron-ffmpeg.yaml
```

## Distributed jobs

We need to modify bash command if we want to run more than one job pod or there will be race condition errors.
So, use [job-distributed-ffmpeg.yaml](job-cron-ffmpeg.yaml):

Here\
`parallelism: 4`: number of jobs running in parallel\
`sleep 1` in bash command: to let all pods do the job

Run the job and see the logs on one of the pods after job is done

```
kubectl create -f ./job-cron-ffmpeg.yaml
pods=$(kubectl get pods --selector=job-name=converter --output=jsonpath={.items..metadata.name} | awk '{print $1}'); kubectl logs $pods
```

You will see only some lines with numbers, so this pod handled only part of "queue".

Delete job

```
kubectl delete -f ./job-distributed-ffmpeg.yaml
```