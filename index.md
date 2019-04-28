# topocity ![Status Badge - Travis CI](https://travis-ci.com/ennioVisco/topocity.svg?branch=master)

_Note: Open-source version at [https://github.com/ennioVisco/topocity](https://github.com/ennioVisco/topocity)_

__Topocity__ is the prototypical implementation we developed to complement theoretical analysis presented by our research paper.



## Usage Guidelines
This guide provides a quick walk-through for the usage of our framework within the provided VM.
For installations from scratch, refer to the online instructions.

After launching the VM in VirtualBox, log in by user: __yves__, password: __klein__.

After opening a command prompt, go to the `src` folder by executing:

```
cd ~/Desktop/topocity/src
```

Then launch the interpreter on the library entry-point:

```
stack ghci Lib.hs
```

To experiment with `topocity`, you can execute the following commands in the REPL.

*__WARNING__: Current default XML parser is highly memory-eager: avoid operating on the data from the folder `/2/` unless AT LEAST 16GB are available for the machine.*

### Loading the CityGML _Source_

```haskell
source = load "1/original.gml" "1/ade.gml"
```

### Showing the result of _Get_

```haskell
view = get source -- performs the forward BX: CityGML -> Bigraph
display view'' -- prints in stdout the internal representation of the graph
```

### Changing the _View_

Wrappers to simulate changes in the view

```haskell
view'  = addBuilding "demo1" view
view'' = removeBuilding "bc8a0f2b5-031b-11e6-b420-2bdcc4ab5d7f" view'
display view'' -- prints in stdout the internal representation of the graph
```

### Reflecting the changes back to source with _Put_

```haskell
source' = put source view''  -- performs the putback BX: CityGML <- Bigraph
```

### Storing back the new _Source_

```haskell
store source' "1_out.gml" "1_aout.gml" -- Stores the new CityGML and ADE files
```

### Quickly check the changes
To check the changes when no gml viewer is available, one could use the diff tool, for example:
```
diff -u ../in/0/original.gml ../out/out.gml
```

# Customization
Note that input files are taken from the `topocity/in` directory while output files are generated into the `topocity/out` directory.

To change this, change the paths in `topocity/src/Settings.hs` variables.

The following commands use files provided with this repository, however other input can be used, despite currently there is a very limited support of CityGML features related to the current state of development of the [citygml4hs][4d6757c3] library.

[4d6757c3]: https://github.com/ennioVisco/citygml4hs "citygml4hs"

[927a319c]: https://www.graphviz.org/ "GraphViz"

[45cc488c]: https://haskellstack.org "Haskell Stack Website"

[5d8ff35d]: https://bitbucket.org/prl_tokyo/bigul/ "BiGUL: The Bidirectional Generic Update Language"
