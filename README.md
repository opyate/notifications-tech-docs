# GOV.UK Notify – Technical Documentation

## Getting started

### Docker container

This app uses dependencies that are difficult to install locally. In order to make local development easy, we run app commands through a Docker container. Run the following to set this up:

```shell
make bootstrap-with-docker
```

Because the container caches things like packages, you will need to run this again if you change the package versions.

## To run the application

```
make run-with-docker
```

If all goes well something like the following output will be displayed:

```
== The Middleman is loading
== LiveReload accepting connections from ws://192.168.0.8:35729
== View your site at "http://Laptop.local:4567", "http://192.168.0.8:4567"
== Inspect your site configuration at "http://Laptop.local:4567/__middleman", "http://192.168.0.8:4567/__middleman"
```

You should now be able to view a live preview at http://localhost:4567.

## To test the application

```
make test-with-docker
```

## Making changes

To make changes edit the source files in the `source` folder.

Although a single page of HTML is generated the markdown is spread across
multiple files to make it easier to manage. They can be found in
`source/documentation`.

A new markdown file isn't automatically included in the generated output. If we
add a new markdown file at the location `source/documentation/agile/scrum.md`,
the following snippet in `source/index.html.md.erb`, includes it in the
generated output.

```
<%= partial 'documentation/agile/scrum' %>
```

Including files manually like this lets us specify the position they appear in
the page.

## Deployment

The tech docs are built and deployed in a concourse pipeline, using a container image built from the Dockerfile at the root of this repository.

If tech docs fail to deploy and the container needs to be updated, run the `build-tech-docs-image` task in Concourse after making and committing any required changes to the Dockerfile.

## Licence

Unless stated otherwise, the codebase is released under [the MIT licence](./LICENSE).

The data is [© Crown
copyright](http://www.nationalarchives.gov.uk/information-management/re-using-public-sector-information/copyright-and-re-use/crown-copyright/)
and available under the terms of the [Open Government
3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)
licence.
