# Question (AWS Day 28)

The Nautilus DevOps team has been tasked with setting up a containerized application. They need to create a private Amazon Elastic Container Registry (ECR) repository to store their Docker images. Once the repository is created, they will build a Docker image from a Dockerfile located on the aws-client host and push this image to the ECR repository. This process is essential for maintaining and deploying containerized applications in a streamlined manner.
Create a private ECR repository named devops-ecr. There is a Dockerfile under /root/pyapp directory on aws-client host, build a docker image using this Dockerfile and push the same to the newly created ECR repo, the image tag must be latest.

# Solution

```
aws-client ~ ➜  pwd
/root

aws-client ~ ➜  cd pyapp/

aws-client ~/pyapp ➜  ls
app.py  Dockerfile  requirements.txt

aws-client ~/pyapp ➜  aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 278810891986.dkr.ecr.us-east-1.amazonaws.com

WARNING! Your credentials are stored unencrypted in '/root/.docker/config.json'.
Configure a credential helper to remove this warning. See
https://docs.docker.com/go/credential-store/

Login Succeeded

aws-client ~/pyapp ➜  cat /root/.docker/config.json 
{
        "auths": {
                "278810891986.dkr.ecr.us-east-1.amazonaws.com": {
                        "auth": "QVdTOmV5SndZWGxzYjJGa0lqb2lNVk51ZUVJMVprVjRObXhsZVVFeU9VNU1kbkJrU25odGIycE9OVFF3THpGSWIzVjRSMFphYm1kcldYUTFVbmwzYUhWV09HbzBOakkwV0dkeWJrbFljM1phTVRaSVVubFVXSEp5T1U1RFluaFJkMFJXV0U1NVJ5OVdMemhEUkZSeE9XUTJVbkpYYkVJMU1rYzBlbVJKVm1SMmExRjJOemR6VmxVM1NGcEJhemRUWTJoTGJWRTVWVlprVWtadFpFZDRPV0UxTHpoTVF5c3ZVakZ1Wldsak5IUklOSEZETmtkSlExcDJabmhOTXk4NVJVbEJkRzgzWWxKNlJ5czNTRFpOY21WTWEzbEVOMFYyYVRoelJuQTVUMEl4VVV4WlJrbzNaa0V4YURCUE4xbENVblF6TUU4dllVSXZhRkFyYnpZeE9ISTJZMUJUVDNCYVVFaEhlVTlhYW1SeVpHaFRkMk12VERWbE9WUktNVmM0U0dSMFpuaHNNREoyWlUxWGNITlBVM053V1hSNlFXRnphUzlRV21WSGVFaG5helVyWkdKUlZtcEliR0pXZEZaRlYzaG9kMnh3U21wMVRrMXlhMkZpUVhsYVVIaGFlWFIzWVU0elJrSlZUU3RYUzFwSk5uSkNWelZaZFRkQlNGbFllVXMxTkM5Q2RVSkxZMFZhUlVObGJHcDRUMkZ1ZERWallYbG5jVUpXYml0dlMwOVZiMlZ0VUU1cVVIa3dUV2hwYkZveE5rSkRMelZUY1cwd1QzVk1PR2syV1hNelpHNXlTWGQ2VjFaNmNWRkRZbFZtUm5KeVRUZEdNa2tyWjBkSGNXdzRNVTlVUlhreU1uRnBVSGREU2tnMU5tRTRRMVowZFdVd1RGUllURmd6ZG5OM05tcDNWbkpMZVU5TlJsQmpNQ3RCYzA1c1IzQkVUMkpZSzBoUFNGRjRRbVF6UmtGSlVXWmpkSHBMU2l0S1oycE9WMGxxZDJOUWFVZEJXWFpGTW1wTmVrZEZTREZtVjBKRWNWbGFjRzVoTUd4NFpuZ3JaVTVxYUVVeFdteFdLMlJXT1ZsdGNWZzFSRlZrY0c4NGNFNDBNbmRxWm1seVNUUndLMmN2T1cxV1FrNTVUV2RHSzIxVWJVMXBSblptTldoUVpUUlNValZaT0ZOb2FuTllVWE5sV0hkRGFuWlVXVzgzU2tOV05FRjJORWRUTld4cVpteHRjbGxuVlRFM2FUUm5NMU5MU0VwSFNrTndTMGhXTjBWRFZrOU5VVVJFY0U1S0sycE9SV3hQUWtnMWJtUlRaWFp0YTBScVMycFdhbTlTV2pKRU1VZHpOR2R3YVZnd05FTkxNVlJOUW5acmR6UlVZbWRsWlcxWlZGaEJURk5JVTNwMVFqZFlOVXcxUVVRcldVSXpiVXRNT1hKT1MwbFhZbkJXY1UxSmMyZHBRVXhJTkdadFJGcFVRbXd3WkdsU2NrczFRVXBZVVdWb2RWbFhLMGxSYVRGUVJtOWhkelozVjNSdldUWmxiVmRKSzBaV1pGcExXRTloWVV0RGVXa3dSVVpaYm5ST2JWRjZha3AxTUVoaFkzSTBTVzVXZERGd1lYWlpUa0ZHY1VoQlZGWlhkbVV3V2xoQ2IwSkZOWEZDY0ZreGFqaHFNa1I2YWpaNFRubEhRVkZGZDBGelpFMU5ORE5hWkRSaVVqSnNReXRLV0VKSVZYSndOVVJsUWsxcmRIVTVSazVTVWxWRWJGUmpVRkJhU0hKYVNEVmFPU3RvUzFCcmVVOURXblpVZEZRelJITjFkM2hOWlc5RFZuWlBORTE0VEhwYVpreGFlRk51UTFjMlRVRkhNQ0lzSW1SaGRHRnJaWGtpT2lKQlVVVkNRVWhvZDIwd1dXRkpVMHBsVW5SS2JUVnVNVWMyZFhGbFpXdFlkVzlZV0ZCbE5WVkdZMlU1VW5FNEx6RTBkMEZCUVVnMGQyWkJXVXBMYjFwSmFIWmpUa0ZSWTBkdlJ6aDNZbEZKUWtGRVFtOUNaMnR4YUd0cFJ6bDNNRUpDZDBWM1NHZFpTbGxKV2tsQlYxVkVRa0ZGZFUxQ1JVVkVUWGhEUkZSS2NYVkRVbWhHTVRsQk5IZEpRa1ZKUVRjd09XNW1SMEZqV1Zvd1JHbHhNbTVIZUZNMlVVVkxkbVJ6V1hOMmIxUTJWREIzVDFWRmN6azVaV2R2YTAxdE9GbExjRFJGTmxSaFZub3ZNbFZzYzNsdlpXRnlORFJVTVRGWlNDdFRZVTFqUFNJc0luWmxjbk5wYjI0aU9pSXlJaXdpZEhsd1pTSTZJa1JCVkVGZlMwVlpJaXdpWlhod2FYSmhkR2x2YmlJNk1UYzNOekkyTWpVMU0zMD0="
                }
        }
}
aws-client ~/pyapp ➜  docker build -t devops-ecr .
[+] Building 188.4s (9/9) FINISHED                                    docker:default
 => [internal] load build definition from Dockerfile                            0.1s
 => => transferring dockerfile: 164B                                            0.0s
 => [internal] load metadata for docker.io/library/python:3.8-slim            122.6s
 => [internal] load .dockerignore                                               0.1s
 => => transferring context: 2B                                                 0.0s
 => [internal] load build context                                               0.1s
 => => transferring context: 259B                                               0.0s
 => [1/4] FROM docker.io/library/python:3.8-slim@sha256:1d52838af602b4b5a831b  62.0s
 => => resolve docker.io/library/python:3.8-slim@sha256:1d52838af602b4b5a831be  0.1s
 => => sha256:030d7bdc20a63e3d22192b292d006a69fa3333949f536d6 3.51MB / 3.51MB  30.9s
 => => sha256:1d52838af602b4b5a831beb13a0e4d073280665ea7be7f 10.41kB / 10.41kB  0.0s
 => => sha256:314bc2fb0714b7807bf5699c98f0c73817e579799f2d9156 1.75kB / 1.75kB  0.0s
 => => sha256:b5f62925bd0f63f48cc8acd5e87d0c3a07e2f229cd2fb0a9 5.25kB / 5.25kB  0.0s
 => => sha256:302e3ee498053a7b5332ac79e8efebec16e900289fc1e 29.13MB / 29.13MB  31.3s
 => => sha256:a3f1dfe736c5f959143f23d75ab522a60be2da902efac 14.53MB / 14.53MB  31.1s
 => => sha256:3971691a363796c39467aae4cdce6ef773273fe6bfc67154d01 248B / 248B  61.5s
 => => extracting sha256:302e3ee498053a7b5332ac79e8efebec16e900289fc1ecd1c754c  1.2s
 => => extracting sha256:030d7bdc20a63e3d22192b292d006a69fa3333949f536d62865d1  0.1s
 => => extracting sha256:a3f1dfe736c5f959143f23d75ab522a60be2da902efac236f4fb2  0.6s
 => => extracting sha256:3971691a363796c39467aae4cdce6ef773273fe6bfc67154d01e1  0.0s
 => [2/4] COPY . /app                                                           0.2s
 => [3/4] WORKDIR /app                                                          0.2s
 => [4/4] RUN pip install -r requirements.txt                                   2.8s
 => exporting to image                                                          0.3s 
 => => exporting layers                                                         0.2s
 => => writing image sha256:a3ed0de5b6d2c2078f7e87082bcace7ca362cea2ab6ce157e8  0.0s
 => => naming to docker.io/library/devops-ecr                                   0.0s

aws-client ~/pyapp ➜  docker tag devops-ecr:latest 278810891986.dkr.ecr.us-east-1.amazonaws.com/devops-ecr:latest

aws-client ~/pyapp ➜  docker push 278810891986.dkr.ecr.us-east-1.amazonaws.com/devops-ecr:latest
The push refers to repository [278810891986.dkr.ecr.us-east-1.amazonaws.com/devops-ecr]
572242a529eb: Pushed 
5f70bf18a086: Pushed 
a5238f032019: Pushed 
d2a2207b52a4: Pushed 
5d2d143f3d7f: Pushed 
c3772b569c3a: Pushed 
8d853c8add5d: Pushed 
latest: digest: sha256:e28fcfa8f12a69a51493b90b2b2db9afcd537075d033fe668b17cb85b099d618 size: 1783

aws-client ~/pyapp ➜ 
```
