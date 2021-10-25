Here is a quick and easy dockerfile which runs a small dash app: https://github.com/kyso-io/docker-dash. I'd like you to create a rest api server which accepts posts requests to run this docker container in the cloud (you will probably need to build the image and host it somewhere), and to save logs of the container runs in mongodb.

Please use these api routes:

1. `/start` - when this route is hit run the above docker file on an online hosted container service (ECS, hosted Kubernetes etc - use the free plan!). Please run the container in a publicly addressable way. If the container is already running or in the process of starting or stopping this route should return an error. Every start should be a fresh install of the container. It doesn't need to be built everytime, but it should be a fresh instance of the container (not just a restart of a container already installed on a machine). This should also make an entry in a mongodb collection showing the start time of the container.

2. `/stop` - this should stop the container, if the container is already stopping or starting this should return an error. This should also edit the entry in the mongodb collection adding the stop time of the container.

3. `/status` - this will return the status of the container, off, starting, running, stopping, error, and if running it should return the url of the container. If the status has an error it should attempt to give extra information on the error.

For example, making a status request to your api using httpie could look like this:

```
>>> http post <your-url>/start

{
    "status": "running",
    "url": "https://some-web-url:port"
}
```

The mongo records would look something like this:

```
{ container_id: "asdfwff343fq334qg", start_time: "some start time", stop_time: "some stop time" },
{ container_id: "f24imoreignseoger", start_time: "some start time", stop_time: "some stop time" },
{ container_id: "rojgnselritgjn4i5", start_time: "some start time", stop_time: "some stop time" },
{ container_id: "awekjgfnawgjnser", start_time: "some start time", stop_time: null } // still running.
```

Some extra conditions:

- The API should only accept and return JSON, not xml.
- Please use nodejs.
- Please structure your project as a github repo, when you're ready to submit please add me to the project (https://github.com/eoinmurray).
- You don't need to host your api, but it helps if you make a url somewhere that I can just hit with some test requests. I can run it locally myself when you submit if needed, in that case please give detailed instructions if I need api keys etc, how to setup mongo etc.
- I estimate that this should only take a few hours, all going well.
