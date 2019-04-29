# Example werf.io and golang 1.12
> Simple

## Build
1. Install werf (I used 1.0.4-beta.4)
    ```bash
    curl -L https://dl.bintray.com/flant/werf/v1.0.1-beta.4/werf-linux-amd64-v1.0.1-beta.4 -o /tmp/werf
    chmod +x /tmp/werf
    sudo mv /tmp/werf /usr/local/bin/werf
    ```
2. Git clone this repo
   ```bash
   git clone https://github.com/zhilyaev/werf-example.git
   ```
3. Set --stages-storage default value using $WERF_STAGES_STORAGE param
    ```bash
    export WERF_STAGES_STORAGE=:local
    ```
4. Main build 
    ```bash 
    werf build
    ```
5. Enjoy
    ```bash
    $ docker images                                                         
    REPOSITORY                    TAG                                                                IMAGE ID            CREATED             SIZE
    werf-stages-storage/project   a33d8a20716fcb2f749ee19443c0bf555b55ce8fce304431ca81153a2e53f7c5   fe747a108218        About an hour ago   17.1MB
    werf-stages-storage/project   413e929a140d1bc687cfae981e950dcd45cbfbf7ed578b77d1400c70a66fb440   165090988574        About an hour ago   17.1MB
    werf-stages-storage/project   90d3ecbeca001eb210791fac47c264b9058c0d208296a39840194fd999de4544   4dd9437ba342        About an hour ago   648MB
    werf-stages-storage/project   04a6275f1f6b36c6d3fb7714bcb9cd3964e289fa54ad7b294aee0e33c819f61f   e57e30d253ed        About an hour ago   637MB
    werf-stages-storage/project   79c9350e57edf59ab8e89647dfdd5f022923a2672f8c1ec12e1b1a20f6972ae7   936d0907738e        About an hour ago   17.1MB
    werf-stages-storage/project   2acd4a4ca5d3e42d144dca4f52514b67fe536d1046a40e0c862b6c34a27690fe   5d69d82b78d6        About an hour ago   17.1MB
    werf-stages-storage/project   20acb131ef06185b8a5cc74dce8eed8bbb1a88969e9af59d1f3cbed749693b18   d2380f73a521        About an hour ago   5.53MB
    werf-stages-storage/project   dd650f573460232b043c5bee6ba3dfafdf36f1cec16f2aebc44ffa750ff56035   cb59febc835c        About an hour ago   648MB
    werf-stages-storage/project   4abb7692d074d46c32d4ca19d2ca4bed123ac7aa573cbbdb3283eabe3b44f7bd   0edf9a9740b9        About an hour ago   637MB
    werf-stages-storage/project   9d6eb7bcb159b0dd2ae057a32eef94113c7b516ebc339a1f5c6dfd0c0ff3c687   469dae8d128b        About an hour ago   637MB
    werf-stages-storage/project   3294bc49d6c75d88f9f85165c6a50e24a630da55596e6ed84d2c7a16eb77d03f   20a56ce200dd        About an hour ago   525MB
    werf-stages-storage/project   cda741cc35c1919bf3b752ceb85340ff49c5538ae47db19f8ae867df8fd1da74   2def7c76f0bd        About an hour ago   525MB
    werf-stages-storage/project   85d55bae26f858c205f6c8e39f5b4cdc9904558517e600421a20ee148e5ef137   3babd9476715        About an hour ago   350MB
    ```

## Run
Run with werf:
```bash
werf run prod --docker-options="-d -p 3000:3000"   
```
The command above run something like that:
```bash
docker run -d -p 3000:3000 werf-stages-storage/project:a33d8a20716fcb2f749ee19443c0bf555b55ce8fce304431ca81153a2e53f7c5
```

Try to connect
```bash
$ curl localhost:3000
Hello, World!%     
```


## Publish
1. Start Docker registry locally
    ```bash
    docker run -d -p 5000:5000 --restart=always --name registry registry:2
    ```
2. Publish with werf:
    ```bash
    werf images publish --images-repo localhost:5000/app --tag-git-branch master 
    ```
3. Try to connect
    ```bash
    $ curl -X GET localhost:5000/v2/_catalog                                                                                                                                                                                                                                                                     
    {"repositories":["app/prod"]}
     ``` 