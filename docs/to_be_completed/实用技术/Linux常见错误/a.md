
# error pulling image configuration: download failed after attempts=6: dial tcp ip:443: i/o timeout

```bash
username@host:~/Downloads/gitlab_ce$ docker-compose up -d
WARNING: The GITLAB_HOME variable is not set. Defaulting to a blank string.
Pulling web (gitlab/gitlab-ee:latest)...
latest: Pulling from gitlab/gitlab-ee
3f94e4e483ea: Retrying in 5 seconds
3f94e4e483ea: Retrying in 1 second
ad7666d95e9d: Retrying in 1 second
3f94e4e483ea: Retrying in 1 second
ad7666d95e9d: Retrying in 1 second
c13c9ef9b3a6: Retrying in 1 second
5f7feec49f24: Waiting
8f32509c0341: Waiting



ERROR: error pulling image configuration: download failed after attempts=6: dial tcp ip: i/o timeout
```
