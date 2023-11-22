---
title: "Globus"
linkTitle: "Globus"
weight: 40
description: >
  File transfer with Globus
tags:
- rivanna
- linux
- filetransfer
---

# Getting the Cosmoflow data via globus commandline 

## Data Directory 

We will showcase how to transfer data via globus
commandline tools.

In our example we will use the data directory as

```bash
export DATA=/project/bii_dsc_community/$USER/cosmoflow/data
```

## Globus Set Up on Rivanna

Rivanna allows to load the Globus file transfer command line tools via
the modules command with the following commands. However, prior to
executing globus login, please visit <https://www.globus.org/> and log
in using your UVA credentials.

```bash 
module load globus_cli
globus login
```

The `globus login` method will output a unique link per user that you
should paste into a web browser and sign in with using your UVA
credentials. Afterwords, the website will present you with a unique
sign-in key that you will need to paste back into the command line to
verify your login.

After executing `globus login` your console should look like the
following block.

> NOTE: this is a unique link generated for the example login,
> each user will have a different link.

```
-bash-4.2$globus login
Please authenticate with Globus here:
------------------------------------
https://auth.globus.org/v2/oauth2/authorize?client_id=affbecb5-5f93-404e-b342-957af296dea0&redirect_uri=https%3A%2F%2Fauth.globus.org%2Fv2%2Fweb%2Fauth-code&scope=openid+profile+email+urn%3Aglobus%3Aauth%3Ascope%3Aauth.globus.org%3Aview_identity_set+urn%3Aglobus%3Aauth%3Ascope%3Atransfer.api.globus.org%3Aall&state=_default&response_type=code&access_type=offline&prompt=login
------------------------------------

Enter the resulting Authorization Code here:
```

Follow the url and input the authorization code to login successfully.

## Source Endpoint Search


First, verify that you were able to sign in properly, and verify your
identity and then search for the source endpoint of the data you want
to transfer. In this example, our endpoint is named `CosmoFlow
benchmark data cosmoUniverse_2019_02_4parE`. Please note that the file
to be downloaded is 1.7 TB large. Make sure that the system on which
you download it has enough space. The following commands
will verify your sign in identity and then search for an endpoint
within the single quotation marks.

```bash
globus get-identities -v 'youremail@gmailprobably.com'
globus endpoint search 'CosmoFlow benchmark data cosmoUniverse_2019_02_4parE'
```

Each globus endpoint has a unique endpoint ID. In this case our source endpoint ID is:

* `d0b1b73a-efd3-11e9-993f-0a8c187e8c12`

Set up a variable `ENDPOINT` so you can use the endpoint more easily without retyping it. 
Also set a variable `SRC_DIR` to indicate the directory with the files to be transferred.

```bash
export SRC_ENDPOINT=d0b1b73a-efd3-11e9-993f-0a8c187e8c12
export SRC_DIR=/~/
```

You can look at the files in the globus endpoint using `globus ls` to
verify that you are looking at the right endpoint.

```bash
globus ls $SRC_ENDPOINT
```

## Destination Endpoint Set Up

Rivanna HPC has set a special endpoint for data transfers into the
`/project`, `/home`, or `/scratch` directories. The name of this
destination endpoint will be `UVA Standard Security Storage`.

Repeat the above steps with this endpoint and set up the variables
including a `path` variable with the desired path to write to.

```bash
globus endpoint search 'UVA Standard Security Storage'
export DEST_ENDPOINT=e6b338df-213b-4d31-b02c-1bc2c628ca07
export DEST_DIR=/dtn/landings/users/u/uj/$USER/project/bii_dsc_community/uja2wd/cosmoflow/
```

> NOTE: We cannot set the path to start at the root level in rivanna 
> and instead need to follow a few steps to find the specific path of 
> where to write to. 
>
> To begin, our path must start with `/dtn/landings/users/` 
> and is then appended on a unique sequence depending on the users computing ID. 
> The rest of the path is dependent on characters of the users computing ID.
> As an example, if your computing ID is abc5xy, the next three arguments are
> `/a/ab/abc5xy` (first char, first two chars, computing id), at this point the 
> user is essentially in the root level of rivanna and can access 
> `/home`, `/project`, or `/scratch` how they normally would.
---
> Note: If you want to use the web format of Globus to find the path isntead. 
> Follow the below steps to find the desired value of your path var.
 
* First sign into the web format of globus
* Locate `file manager` on the left side of the screen
* In the `collections` box at the top of the screen begin to search
  for `UVA Standard Security Storage`
* Select our destination endpoint
* Use the GUI tool to select exactly where you wish to write to
* Copy the path from the box immedietally below `collections`
* Write this value to the DEST_DIR variable created above (I have
  included my path to where I wish to write to)

## Initiate the Transfer

Finally, execute the transfer

```bash
globus transfer $SRC_ENDPOINT:$SRC_DIR $DEST_ENDPOINT:$DEST_DIR
```

NOTE: In case your first transfer may have an issue because you need to give
globus permission to initiate transfers via the CLI instead of via the
web tool. I was given the unique command as follows by my terminal:

```bash
-bash-4.2$globus transfer $SRC_ENDPOINT:$SRC_DIR $DEST_ENDPOINT:$DEST_DIR
```

```
The collection you are trying to access data on requires you to grant
consent for the Globus CLI to access it.  message: Missing required
data_access consent
```

Please run

```
  globus session consent 'urn:globus:auth:scope:transfer.api.globus.org:all[*https://auth.globus.org/scopes/e6b338df-213b-4d31-b02c-1bc2c628ca07/data_access]'
  ```
  
to login with the required scopes


After initiating this command, a similar sign in a verification will
be conducted compared to the `globus login` method where the cli will
output a url to follow, the user will sign in, and return a
verification code.

After fixing this, remember to re-initiate the transfer with the

`globus transfer`

command as previously descibed.

## Managing Tasks

To monitor the status of active transfers, use 

```bash
globus task list
```

or similarly you can use the web tool to verify transfers.

## References:

1. Globus Data Transfer, Rivanna HPC <https://www.rc.virginia.edu/userinfo/globus/>
