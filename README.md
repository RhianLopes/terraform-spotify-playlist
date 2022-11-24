# terraform-spotify-playlist

[Tutorial Link](https://developer.hashicorp.com/terraform/tutorials/community-providers/spotify-playlist)


## :fire: Run

Is necessary create a `.env` file with these info.

```
SPOTIFY_CLIENT_ID=<your client id>
SPOTIFY_CLIENT_SECRET=<your client secret>
```

Run a spotify auth proxy container.

```shell
$ docker run --rm -it -p 27228:27228 --env-file ./.env ghcr.io/conradludgate/spotify-auth-proxy 
APIKey:   xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
Auth URL: http://localhost:27228/authorize?token=xxxxx
```

Access the output Auth URL and do the spotify login. In success case, will output this message: `Authorization successful`.

Create another file `terraform.tfvars` like this.

```
spotify_api_key = "<your api key : xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx>"
```

Finally, run.

```shell
$ terraform init
```

And 

```shell
$ terraform apply
data.spotify_search_track.by_artist: Reading...
data.spotify_search_track.by_artist: Read complete after 0s [id=1669260398]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # spotify_playlist.playlist will be created
  + resource "spotify_playlist" "playlist" {
      + description = "This playlist was created by Terraform"
      + id          = (known after apply)
      + name        = "Terraform Summer Playlist"
      + public      = true
      + snapshot_id = (known after apply)
      + tracks      = [
          + "2Z8yfpFX0ZMavHkcIeHiO1",
          + "7JJmb5XwzOO8jgpou264Ml",
          + "3zkWCteF82vJwv0hRLba76",
        ]
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + playlist_url = (known after apply)

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

spotify_playlist.playlist: Creating...
spotify_playlist.playlist: Creation complete after 1s [id=7kFsU0EiM0FNqmKHS1OJq0]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

Outputs:

playlist_url = "https://open.spotify.com/playlist/7kFsU0EiM0FNqmKHS1OJq0"
```

Check my first [spotify playlist provising by terraform s2](https://open.spotify.com/playlist/7kFsU0EiM0FNqmKHS1OJq0).
