# yaml-compose

This project was created to solve a common problem when working with YAML files,
my intention with this tool is to instead having a big YAML file we are able to have
little ones and merge in a single file with a very simple structure.

The script is written in `Groovy` so you need to verify if you have installed in your path.

## Usage

Think in the following sample where you have some yaml files

`sample-1.yml`
```yaml
property-1:
    something: 'value'
property-2:
    something-else: 'another-value'
```

And in another file you have this:

`sample-2.yml`
```yaml
property-3:
    something: 'new value'
```

If you want to create a single file create a template like this:

`my-custom-template.yml`
```yaml
my-common-property: 'sample'
another-common: 'whatever you want'

list-of-includes:
    $include: sample-1.yml
    $include: sample-2.yml
```

The `$include` will be replaced by the file and will use the same level where was found.

```
yaml-compose -i my-custom-template.yml
```

The result will be created on the same directory in the file`output.yml`
```yaml
my-common-property: 'sample'
another-common: 'whatever you want'

list-of-includes:
    property-1:
        something: 'value'
    property-2:
        something-else: 'another-value'
    property-3:
        something: 'new value'
```

To see some more complex sample look at `sample` folder.

## Parameters
```
> yaml-compose -h

usage: yaml-compose -[hvroi]
 -h,--help           Usage Information
                     
 -i,--input <arg>    name of the yaml file to process [required]
 -o,--output <arg>   output filename by default output.yml
 -r,--recursive      recursively look in the other files for inclusions
 -v,--version        shows the version of the script

```

## Install

Download the project and the give execution permission to the `yaml-compose` script.

```
chmod +x yaml-compose
```

If you want to have available the script in your system you can copy this to your `/usr/local/bin`

**Note: This tool is still on beta if you want to contribute please contact me http://joxebus.github.io**