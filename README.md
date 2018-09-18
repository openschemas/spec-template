# Bioschema Container

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
You now can generate your specification files with the provided Docker container! 

#### Ask for Help
If you need to ask for help, just run the container:

```bash
$ docker run openbases/builder-bioschema
Usage:


         docker run <container> [demo|start|help]
         docker run <container> demo
         docker run <container> help
         docker run -v /code/:/data <container> start

         Commands:

                help: show help and exit
                run:   generate a specification, with your subdirectory with the
                       specifications top level folder bound to /data
                demo: show a demo generation using files in the container
         
         Options [run]:

            --config CONFIG     configuration.yml file, defaults to configuration.yml in
                                folder
            --folder SPECS      folder with input specification subfolders
            --output OUTFOLDER  folder to write output specification subfolders
```

### What Happens in the Continuous Integration?

For a demo, you can see instructions in the [openbases/builder-bioschema](https://www.github.com/openbases/builder-bioschema) repository. This is how we use that
container in the continuous integration (although we can't run with binds so
we copy files instead).


```bash
$ docker run -it -v /tmp/src:/data openbases/builder-bioschema run -
```

Output files, by default, are written to a folder docs/output_files in `/tmp/src`

```
$ docker run -it -v $PWD:/data openbases/builder-bioschema run --config /data/specifications/configuration.yml --output /data/outfiles
```

Here are your files!

```bash
$ tree outfiles/
outfiles/
└── DataCatalog
    ├── examples
    │   └── README.md
    ├── README.md
    └── specification.html
```

Now you know how to do your own!

### Contribute to bioschemas

When you have your finished folder, fork the bioschemas repository,
clone your fork, checkout a new branch, and add your folder
to the folder "specifications". Then issue a pull request!

```bash
git clone https://www.github.com/<username>/specifications
cd specifications
git checkout -b add/spec-datacatalog
```
add your folder, e.g. DataCatalog, to "specifications"

```bash
cp -R <generation_folder>/specifications/DataCatalog $PWD
git add DataCatalog
```

Then open a pull request to the [main repository](https://github.com/BioSchemas/specifications).

## Can we make this easier?

Yes! We will provide a continuous integration template (soon) for you to do this,
likely in the next few days.

## Development

Build the container

```bash
$ docker build -t openbases/builder-bioschemas .
```
