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
3. `export WERF_STAGES_STORAGE=:local`
4. `werf build`