# Docker Image Security Best Practices

Today, in modern era the application development has become so much fast paced and release cycles are more frequent. With earlier approach of deployment strategies, these releases cannot be managed and ultimately end up in losing customers.

With evolution of Containers and orchestration tools, deployment was able to race up to the pace of development. However with this pace, definitely some security flaws that don’t catch our eyes can ruin our day.

Here I will describe 4 basic but important security practices that we can enforce to help minimise these security flaws.

## Use Official Image

Most of us use Images from docker hub as base Images in our Docker file. Make sure that the image pulled are official and are from verified developers.
For example, as you can see from the screenshot, official images will have green Official Image tag.
![image](https://user-images.githubusercontent.com/37524392/157165896-7bf5aa0a-d606-4fe5-b45e-9ed809ddf59a.png)

Yes, just like we follow only officially verified celebrity accounts in your social media, make sure your base image is also officially verified 😊

## Use Minimal Base Images

Prefer using alpine images which has fewer OS libraries. Lots of vulnerabilities in your Docker Image can be mitigated if we use alpine images.
Another advantage of using minimal base image is that your Docker Image size will be considerably very less.

For example, pulling from Node.js base image

`FROM node:10-alpine`

### Recommendation: Always pin the version in Base Image so that your image won’t break if there is any update.

Below screenshot shows how much difference it makes. Please do check the number of layers and its sizes.
![image](https://user-images.githubusercontent.com/37524392/157166124-1d1aaafe-fccb-4531-a149-c3862eb6ed24.png)

![image](https://user-images.githubusercontent.com/37524392/157166139-554e07b1-a982-4eff-85f0-8539206b3f2f.png)

## Find and fix Open Source Vulnerabilities

Regularly Scan your Docker Image for Open Source Vulnerabilities.

Anchore Engine is a great scanner tool that you can use to scan your Image Vulnerabilities. Anchore engine provides an inline scanner which can be integrated with your CI pipelines. This [blog](https://anchore.com/blog/inline-scanning-with-anchore-engine/) explains how you can integrate anchore engine with various CI tools.

Further you can install anchore-engine and do a regular scan of your deployed docker images.
For more details on how to install and use anchore engine, you can go through [this](https://github.com/anchore/anchore-engine).

## Use Linter to Dockerfile

Enforce Dockerfile best practices automatically by using a static code analysis tool such as [hadolint](https://github.com/hadolint/hadolint) linter, that will detect and alert for issues found in a Dockerfile.

It is always better to add hadolint in your CI pipeline itself, so that we catch the problems earlier.
Before even that, we should also have some kind of understanding on writing a Dockerfile properly. For that [read here](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/).

## Conclusion

Here I explained some practices that you can easily implement to ensure basic security before deployment. There are so many other important practices you should be following which I will be writing about in future write ups.

Hope this article help to strengthen the basic security practices. Happy day !
