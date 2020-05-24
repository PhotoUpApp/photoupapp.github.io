<br>
# Installing Rclone and PhotoUp

Using the official [documentation](https://rclone.org/install/). All major operating systems are supported (Linux, MacOS, Windows).

For a quick setup, **download the appropriate Windows binary** from [here](https://rclone.org/downloads/), or **run the following command for Linux or MacOS**:

```
curl https://rclone.org/install.sh | sudo bash
```

You can download PhotoUp from [here](https://github.com/PhotoUpApp/app/releases) to help you interact with Rclone.


<br>
# Configuring Rclone

This can be done from the command line or by using the following configuration file.

<br>
## Configuring Google Photos source

**Before running these steps, make sure you first have a Google account.**

### 1. Run `rclone config` and select option to add a `New Remote` (n)
```
$ rclone config

e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> n
```

### 2. Type `GooglePhotos` as **Name**
```
name> GooglePhotos
```

### 3. Select (write) `google photos` as storage type
```
Type of storage to configure.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / 1Fichier
   \ "fichier"
 2 / Alias for an existing remote
   \ "alias"
[...]
Storage> s3
```

### 4. Skip (Press Enter) setting Google Application Client Id
```
Google Application Client Id
Leave blank normally.
Enter a string value. Press Enter for the default ("").
client_id>
```

### 5. Skip (Press Enter) setting Google Application Client Secret
```
Google Application Client Secret
Leave blank normally.
Enter a string value. Press Enter for the default ("").
client_secret>
```

### 6. Do not set (Press Enter) read-only permissions
```
Set to make the Google Photos backend read only.

If you choose read only then rclone will only request read only access
to your photos, otherwise rclone will request full access.
Enter a boolean value (true or false). Press Enter for the default ("false").
read_only>
```

### 7. Skip (Press Enter) the advanced configuration step
```
Edit advanced config? (y/n)
y) Yes
n) No (default)
y/n>
```

### 8. Use Remote config (Press Enter) and follow the instructions in your browser, in order to grant permissions to your google account
```
Remote config
Use auto config?
 * Say Y if not sure
 * Say N if you are working on a remote or headless machine
y) Yes (default)
n) No
y/n>
```

### 9. Confirm (Press Enter) your Google Photos configuration (your config will look different than the example)
```
If your browser doesn't open automatically go to the following link: http://127.0.0.1:53682/auth?state=IP2cOTqDVAMmXj8W-ySMfw
Log in and authorize rclone for access
Waiting for code...
Got code

*** IMPORTANT: All media items uploaded to Google Photos with rclone
*** are stored in full resolution at original quality.  These uploads
*** will count towards storage in your Google Account.

--------------------
[gtest]
type = google photos
token = {"access_token":"XXXXXXXXXXXXXXXXXXXXX","token_type":"Bearer","refresh_token":"XXXXXXXXXXXXXXXXXXXXX","expiry":"2020-05-24T18:48:21.677031+02:00"}
--------------------
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d>
```


<br>
## Configuring AWS S3 source

**Before running these steps, make sure you first create a S3 bucket, by following
these [instructions](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html).**


### 1. Run `rclone config` and select option to add a `New Remote` (n)
```
$ rclone config

e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> n
```

### 2. Type `S3` as **Name**
```
name> S3
```

### 3. Select (write) `s3` as storage type
```
Type of storage to configure.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / 1Fichier
   \ "fichier"
 2 / Alias for an existing remote
   \ "alias"
[...]
Storage> s3
```

### 4. Choose `Amazon Web Services (AWS) S3` (1) as storage provider
```
Choose your S3 provider.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / Amazon Web Services (AWS) S3
   \ "AWS"
[...]
provider> 1
```

### 5. Choose (write) `false` in order to provide AWS S3 credentials now
```
Get AWS credentials from runtime (environment variables or EC2/ECS meta data if no env vars).
Only applies if access_key_id and secret_access_key is blank.
Enter a boolean value (true or false). Press Enter for the default ("false").
Choose a number from below, or type in your own value
 1 / Enter AWS credentials in the next step
   \ "false"
 2 / Get AWS credentials from the environment (env vars or IAM)
   \ "true"
env_auth> false
```

### 6. Insert correct `access_key_id` and `secret_access_key` for your AWS S3 bucket
```
AWS Access Key ID.
Leave blank for anonymous access or runtime credentials.
Enter a string value. Press Enter for the default ("").
access_key_id> XXXXXXXXXXXXXX
AWS Secret Access Key (password)
Leave blank for anonymous access or runtime credentials.
Enter a string value. Press Enter for the default ("").
secret_access_key> XXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

### 7. Select a region for S3 which is closest to your location
```
Region to connect to.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
   / The default endpoint - a good choice if you are unsure.
 1 | US Region, Northern Virginia or Pacific Northwest.
   | Leave location constraint empty.
   \ "us-east-1"
   / US East (Ohio) Region
[...]
region> 9
```

### 8. Use default endpoint (Press Enter) for bucket access
```
Endpoint for S3 API.
Leave blank if using AWS to use the default endpoint for the region.
Enter a string value. Press Enter for the default ("").
endpoint>
```

### 9. Set location constraint to same region as previously selected
```
Location constraint - must be set to match the Region.
Used when creating buckets only.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / Empty for US Region, Northern Virginia or Pacific Northwest.
   \ ""
[...]
location_constraint> 9
```

### 10. Select `bucket-owner-full-control` ACL type for access control to bucket
```
Canned ACL used when creating buckets and storing or copying objects.

This ACL is used for creating objects and if bucket_acl isn't set, for creating buckets too.

For more info visit https://docs.aws.amazon.com/AmazonS3/latest/dev/acl-overview.html#canned-acl

Note that this ACL is applied when server side copying objects as S3
doesn't copy the ACL from the source but rather writes a fresh one.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / Owner gets FULL_CONTROL. No one else has access rights (default).
   \ "private"
 2 / Owner gets FULL_CONTROL. The AllUsers group gets READ access.
   \ "public-read"
   / Owner gets FULL_CONTROL. The AllUsers group gets READ and WRITE access.
 3 | Granting this on a bucket is generally not recommended.
   \ "public-read-write"
 4 / Owner gets FULL_CONTROL. The AuthenticatedUsers group gets READ access.
   \ "authenticated-read"
   / Object owner gets FULL_CONTROL. Bucket owner gets READ access.
 5 | If you specify this canned ACL when creating a bucket, Amazon S3 ignores it.
   \ "bucket-owner-read"
   / Both the object owner and the bucket owner get FULL_CONTROL over the object.
 6 | If you specify this canned ACL when creating a bucket, Amazon S3 ignores it.
   \ "bucket-owner-full-control"
acl> 6
```

### 11. Select `None` (1) as server-side encryption
```
The server-side encryption algorithm used when storing this object in S3.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / None
   \ ""
 2 / AES256
   \ "AES256"
 3 / aws:kms
   \ "aws:kms"
server_side_encryption> 1
```

### 12. Select `None` KMS ID
```
If using KMS ID you must provide the ARN of Key.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / None
   \ ""
 2 / arn:aws:kms:*
   \ "arn:aws:kms:us-east-1:*"
sse_kms_key_id> 1
```

### 13. Select `Default` (1) storage class for storing objects
```
The storage class to use when storing new objects in S3.
Enter a string value. Press Enter for the default ("").
Choose a number from below, or type in your own value
 1 / Default
   \ ""
 2 / Standard storage class
   \ "STANDARD"
 3 / Reduced redundancy storage class
   \ "REDUCED_REDUNDANCY"
 4 / Standard Infrequent Access storage class
   \ "STANDARD_IA"
 5 / One Zone Infrequent Access storage class
   \ "ONEZONE_IA"
 6 / Glacier storage class
   \ "GLACIER"
 7 / Glacier Deep Archive storage class
   \ "DEEP_ARCHIVE"
 8 / Intelligent-Tiering storage class
   \ "INTELLIGENT_TIERING"
storage_class> 1
```

### 14. Skip (Press Enter) the advanced configuration step
```
Edit advanced config? (y/n)
y) Yes
n) No (default)
y/n>
```

### 15. Confirm (Press Enter) your S3 configuration (your config will look different than the example)
```
Remote config
--------------------
[S3]
type = s3
provider = AWS
env_auth = false
access_key_id = XXXXXXXXXXXXXX
secret_access_key = XXXXXXXXXXXXXXXXXXXXXXXXXXXX
region = eu-central-1
location_constraint = EU
acl = bucket-owner-full-control
--------------------
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d>
```
