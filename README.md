# DTP - Quick and a bit dirty `.dot` to `.png` automator app.

DTP wraps [graphviz](http://www.graphviz.org/)'s `dot` in an automator application, in order to convert a `.dot` file to a `.png`.

This is done in order to mitigate the fact that at the time of writing (30 IX 2019), on the latest macOS (10.14.6) [graphviz](http://www.graphviz.org/) can't be installed as a stand alone app (see: [the isssue tracker](https://gitlab.com/graphviz/graphviz/issues/1445) and [SO comment](https://stackoverflow.com/questions/43372723/how-to-open-dot-on-mac)) and hence it can't be associated with opening `.dot` filetypes.

The approach used here is a mere workaround, that uses `dot`'s ability to set the desired output format to `.png`, combined with a call to built-in `Preview` application.

## Intended use.

In order to have the application associated with `.dot` files:
* copy the `dtp.app` to `Applications` folder,
* secondary click (right click) a file with `.dot` extension and select `Get Info`,
* in `Open with` drop down select: `Oher...`,
* select `Applications`, then `dtp`, tick `Always Open With` and click `Add`,
* finally, click `Change All...` in the `Get Info` and confirm that you want to apply the change to all documents with extension `.dot`.

If the steps were successful, from now on, double clicking a `.dot` file should result with a `Preview` showing an image that represent the graph.

The steps will set the default open action for the filetype, so commands such `llc`'s `-view-isel-dags` and friends (see llvm link [here](http://llvm.org/docs/ProgrammersManual.html#viewing-graphs-while-debugging-code)) will automatically pick it up.

## Note.

The application hard-codes the location of `dot` binary [here](https://github.com/jchlanda/DTP/blob/master/dtp.app/Contents/document.wflow#L71) (this is the default location used by [`homebrew`](https://formulae.brew.sh/formula/graphviz)). If on your system `dot` lives somewhere else, this line will need to be adapted.

If you see the 
> App can’t be opened because it is from an unidentified developer

message, please see [this article](http://osxdaily.com/2012/07/27/app-cant-be-opened-because-it-is-from-an-unidentified-developer/) for steps needed to have it fixed.
