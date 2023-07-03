---
description: >-
  Since we cannot train the model on the pi, we have to send all of the data we
  collect to the instance we are using for training.
---

# Syncing Data from Pi to Training Node

**Syncing the Data:**

1. In order to allow the pi to connect to the chameleon node, we must give it a key pair to enable an ssh connection.

```
ssh-keygen -t ed25519
```

2. Press enter to whatever prompts come up so that the key is saved in the \~/.ssh folder and there is no passphrase needed to use it.
3. Change the permissions on the private key so that it can be used with ssh

```
chmod 600 ~/.ssh/id_ed25519
```

2. View the public key that was generated can copy the entire key.

```
cat ~/.ssh/id_ed25519.pub
```

_Note: be very careful when selecting the key with your cursor. You want to make sure you are not copying any additional whitespace or leaving out any characters._

4. Back on in the terminal of the training node (you may need to ssh cc@\<ip address> into it again from your own terminal), open the authorized\_keys file.

```
nano ~/.ssh/authorized_keys
```

5. Paste the key you copied at the bottom of this file.
   1. Make sure that when the key is pasted in, it is all on one line and that there are no missing characters or extraneous whitespace
6. Back on the pi, test the ssh connection by running the ssh command to connect to the ip address of the training node. This is the same command you would run on your own computer to connect to the training node.

```
ssh cc@<ip address of training node>
```

7. If the last step was successful, type "exit" to leave the ssh connection and return to the pi.
8. If you have a lot of data, it may be time-efficient to compress the data into a zip file before syncing it.

<pre><code><strong>cd ~/car/data
</strong><strong>zip -r data.zip ~/car/data
</strong></code></pre>

9. Then sync them from the pi to the Chameleon Node:

```
rsync -r ~/car/data/data.zip cc@<Chameleon_Node_Floating_IP_Address>:~/mycar/data
```

_Note: may need to add key before syncing_

```
ssh-add <file path/name of private key>
```

10. Wait for the rsync command to finish (could take a few minutes), then, on the Chameleon node, unzip the data:

```
unzip data.zip -d ~/mycar/data
```

_Note: if the files are not found, it could be due to a wrong saving location and this requires the individual to find their zip file by browsing with UNIX Commands._

\
\
\
\
