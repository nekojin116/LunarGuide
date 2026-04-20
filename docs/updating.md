Last updated: {{ git_revision_date_localized }}


# Updating and Migrating 


## Updating the server

Update the server to get the latest fixes, features, and compatibility changes.

1. Download the latest `Lunar-tear-main.zip` file [here](https://github.com/Walter-Sparrow/lunar-tear/archive/refs/heads/main.zip).
2. Extract the `.zip` into `cage\lunar-tear`, replacing files if prompted.
3. Regenerate protobuf stubs:
    - In `cage/` run:
        ```
        cd lunar-tear\server
        make proto
        ```


## Migrating your progress

If you used the pervious server version, you need to *migrate* your progress into the new database.
In `cage/` run : 

```
cd lunar-tear\server
make migrate
```
