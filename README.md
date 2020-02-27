# Implementing a new exporter for a new services.

If there is another technolgy type the same as the one you are deploying (eg mongo):

1. In jobs/, create a new directory called `<your_service>_exporter/`.
2. Copy/paste all files from previously create other service into this directory.
3. Rename `jobs/templates/<other_service>_exporter_ctl` to `jobs/templates/<your_exporter>_export_ctl`.
4. Find and replace in the the `<your_service>_exporter/` dir, `<other_service>_exporter` for `<your_service>_exporter`.
5. Do the first 4 steps again but for `packages`.
6. With `src/`, create a `<your_service>_exporter/` dir.
7. If there is a similar service, untar the tar.gz located in its `<other_service>_exporter` with `tar -xvzf <other_service>_exporter-<version>.<os>-<arch>.tar.gz`.
8. Tar it back up with the correct name `tar -cvzf <your_service>_exporter-<version>.<os>-<arch>.tar.gz <untarred app>`.
9. Move new tar to `src/<your_service>_exporter/`
10. Push, tag, create rc in concourse and you should be good to go.

However, if you are create an exporter for a service that doesnt exist:
1. Go to [Prometheus bosh-release](https://github.com/bosh-prometheus/prometheus-boshrelease).
2. Read the README and go to the relevant exporter.
3. Ensure you have Golang installed.
4. `go get github.com/<path>`
5. Go to installation at `go/src/github.com/<path>`
6. Read the Makefile, look at release, and follow instructions for linux-amd64 (executables are created for specific architecture you are running locally. Our BOSH vms are running Ubunutu and not OSX)
7. Then go to number 8 above and carry on.
