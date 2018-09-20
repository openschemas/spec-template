# OpenSchema Container

[![CircleCI](https://circleci.com/gh/openschemas/spec-container.svg?style=svg)](https://circleci.com/gh/openschemas/spec-container)

This is an instance of an [openbases](https://openbases.github.io) builder
to generate a schema.org specification using [map2model](https://www.github.com/openschemas/map2model) for the following entities:

 - [Container](specifications/Container)
 - [ContainerImage](specifications/ContainerImage)
 - [ContainerRecipe](specifications/ContainerRecipe)
 - [ContainerDistribution](specifications/ContainerDistribution)

I did the following to generate my container.

 1. Fill in the templates provided on Google Drive, and download as tsv
 2. I added them to the [specifications](specifications) folder here under a subfolder called "Container", along with an entry in [configuration.yml](configuration.yml).
 3. I then hooked up to continuous integration, which automatically ran the [openschemas/schema-builder](https://hub.docker.com/r/openschemas/schema-builder) container that sent my files back to Github pages.
 4. I could then contribute my files via a pull request to [specifications](https://www.github.com/openschemas/specifications). The files that are `*.html` in the subfolders of specifications (e.g., Container, ContainerRecipe) would then be contributed as the specifications to render in the web interface.

For usage, see instructions in the [openschemas](builder-schema) repository.
