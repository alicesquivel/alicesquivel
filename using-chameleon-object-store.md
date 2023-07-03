---
description: >-
  You may want to backup your data and models, especially if you are worried
  your Chameleon lease may end before you are done with the project.
---

# Using Chameleon Object Store

**Chameleon Object Store Usage**

1. Inside of the Chameleon Cloud Node (root directory), there is a README file. This file will contain details about how to mount to the Chameleon object store

```
cat README
```

2. To mount it, run:

```
cc-cloudfuse mount <mounting_dir>
```

example:

```
cc-cloudfuse mount my_mounting_point
```

_Note: Now inside of my\_mounting\_point, it should have all the data you previously pushed to the Chameleon Object Store._

3. Copy all the data from that object store onto the current instance. Replace <> with the actual data directory.

```
cd my_mounting_point
cp -r <data_directory> <filepath_on_this_instance>
```

_Note: now you can use previous data to train the data and leave it for other ML Students to use_

\
\
\
