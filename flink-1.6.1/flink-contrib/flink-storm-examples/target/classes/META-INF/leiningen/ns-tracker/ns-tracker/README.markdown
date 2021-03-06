# ns-tracker

[![Build Status](https://secure.travis-ci.org/weavejester/ns-tracker.png)](http://travis-ci.org/weavejester/ns-tracker)

ns-tracker is a Clojure library for keeping track of changes to source
files and their associated namespaces. This is usually used to
automatically reload modified namespaces in a running Clojure
application.

It is derived from code in Stuart Sierra's [Lazytest][1] tool, and the
credit for writing the vast majority of the code used in this library
should therefore go to him.

[1]: https://github.com/stuartsierra/lazytest

## Installation

As usual, to use this library, add the following dependency to your
`project.clj` file:

    [ns-tracker "0.2.2"]

## Usage

Use the `ns-tracker.core/ns-tracker` function to create a new tracker
function for one or more source directories:

    (use 'ns-tracker.core)

    (def modified-namespaces
      (ns-tracker ["src" "test"]))

When you call the `modified-namespaces` function, it will return a list
of Clojure namespaces that have changed. You can then reload them on
the fly:

    (doseq [ns-sym (modified-namespaces)]
      (require ns-sym :reload))

This can be placed in a background thread, or triggered by some user
request.

## License

Copyright © 2014 James Reeves, Stuart Sierra

Distributed under the Eclipse Public License.
