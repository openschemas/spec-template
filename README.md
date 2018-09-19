# OpenSchema Container

[![CircleCI](https://circleci.com/gh/openschemas/spec-container.svg?style=svg)](https://circleci.com/gh/openschemas/spec-container)

This is an instance of an [openbases](https://openbases.github.io) builder
to generate a bioschemas specification using [map2model](https://www.github.com/vsoch/map2model) for the following entities:

 - [Container](specifications/Container)
 - [ContainerImage](specifications/ContainerImage)
 - [ContainerRecipe](specifications/ContainerRecipe)
 - [ContainerDistribution](specifications/ContainerDistribution)

**under development**

For the map2model repository linked above, see the  `remove-gdrive` 
branch for the code built into container)
to generate specifications for contribution to 
[bioschemas](https://www.github.com/openbases/specifications). 
I did the following to generate my container.

 1. Fill in the templates provided on Google Drive, and download as tsv
 2. I added them to the [specifications](specifications) folder here under a subfolder called "Container", along with an entry in [configuration.yml](configuration.yml).
 3. I then hooked up to continuous integration, which automatically ran the [openbases/openbases-bioschema](https://hub.docker.com/r/openbases/builder-bioschema) container that sent my files back to Github pages.
 4. I could then contribute my files via a pull request to [bioschemas](https://www.github.com/openbases/specifications).

## Usage

### 1. Generate your Front Matter
Edit the file [configuration.yml](specifications/configuration.yml) in 
the [specifications](specifications) directory and fill in the values for your
specification. Are you editing or contributing more than one? Feel free to copy paste the chunk
(not including the "specifications" header) and have more than one.

### 2. Write your specification!
Now generate your new template! You can create a copy of the Google Drive template [provided here](https://docs.google.com/spreadsheets/d/1seHDwKRwET_H8maRTMmdXG7M1deh23Y613TaJ2Pd3qc/edit?usp=sharing).

### 3. Download to your Computer
When you are done, **export each sheet** as a tsv file (tab separated value) and drop into a subfolder named by your specification (e.g., "[DataCatalog](specifications/Datacatalog)" is a folder in [specifications](specifications). When you are done, you will have something like this:

```
specifications/
├── configuration.yml
└── DataCatalog
    ├── DataCatalog - Authors.tsv
    ├── DataCatalog - Bioschemas.tsv
    ├── DataCatalog - Mapping.tsv
    └── DataCatalog - Specification.tsv
```
(with optionally more than one specification subfolder!)

### 4. Generate the specification files
You now can now push your content to Github, and connect to CircleCI to have
the files generated automatically (and deployed to Github pages.) For the deployment
to Github pages you need to:

 1. Create a second Github account to designate as your deployment bot
 2. Give the bot username write access to the repository (add them as a collaborator). You will likely need to open the invite link in a different browser than the one you are logged into with your typical Github username.
 3. Connect the project to CircleCI, and copy paste the project URL also into the second browser (where you can log in with your bot user).
 4. Click "Follow Project" as the bot, and then under Project Settings click on Checkout SSH Keys --> Create and add `<username>` user key

And under "Build Environment" make sure to add the variables for the `GITHUB_USER` and `GITHUB_EMAIL` to correspond with the **bot's**.  There are **no passwords** to be set here!

This will deploy the site to Github pages for the repository, so you will finally need to turn on Github Pages (for the Github Pages branch) of your current repository. That's it! You can also [follow instructions](https://www.github.com/openbases/openbases-bioschema) to just generate the files locally with the 
same Docker container. 


### What Happens in the Continuous Integration?

For a demo, you can see instructions in the [openbases/builder-bioschema](https://www.github.com/openbases/builder-bioschema) repository. This is how we use that
container in the continuous integration (although we can't run with binds so
we copy files instead).

```bash
$ docker run -it -v /tmp/src:/data openbases/builder-bioschema run
```

Output files, by default, are written to a folder docs/output_files in `/tmp/src`,
which the container sees as `/data`

The files typically look like this:

```bash
$ tree outfiles/
outfiles/
└── DataCatalog
    ├── examples
    │   └── README.md
    ├── README.md
    └── specification.html
```

### Contribute to bioschemas

I'm not actually sure how to do this, but when someone responds I hope they can point
me to the right spot. 
