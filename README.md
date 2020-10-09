# PlasticSCM Docker image

⚠ **Warning!** ⚠ **This Docker image is now obsolete. We don't recommend using it in your deployments.** You can take the Dockerfile as a reference to build your own, but it's really out of date at the moment. We apologize for the inconveniences.

To build:

    docker build --rm=true -t <image_name> plastic

To run:

    docker run --name plastic_data <image_name> echo "My data container"
    docker run -d -P --name plastic_server --volumes-from plastic_data <image_name>

To add a user:

    docker run --rm --volumes-from plastic_data <image_name> umtool cu <user_name> <user_password>

To refresh the server:

    docker restart plastic_server

To upload a new license file:

    docker run --rm --volumes-from plastic_data -v $(pwd):/newlicense <image_name> cp /newlicense/plasticd.lic /config

To backup the databases:

    mkdir backup
    docker run --rm --volumes-from plastic_data -v $(pwd)/backup:/backup <image_name> tar cvf /backup/databases_backup_$(date).tar /db/sqlite

To retrieve logs:

    # Console
    docker logs plastic_server
    # Files
    mkdir /log_backup
    docker run --rm --volumes-from plastic_data -v $(pwd)/logs:/log_backup <image_name> tar cvf /log_backup/logs_$(date).tar /logs
