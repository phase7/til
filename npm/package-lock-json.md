## What is package-lock.json

>From [stackoverflow](https://stackoverflow.com/a/44297998/11764123)

It stores an exact, versioned dependency tree rather than using starred versioning like package.json itself (e.g. 1.0.*). This means you can guarantee the dependencies for other developers or prod releases, etc. It also has a mechanism to lock the tree but generally will regenerate if package.json changes.

From [the npm docs](https://docs.npmjs.com/files/package-lock.json):

> package-lock.json is automatically generated for any operations where npm modifies either the node_modules tree, or package.json. It describes the exact tree that was generated, such that subsequent installs are able to generate identical trees, regardless of intermediate dependency updates.
>
> This file is intended to be committed into source repositories, and serves various purposes:
>
> Describe a single representation of a dependency tree such that teammates, deployments, and continuous integration are guaranteed to install exactly the same dependencies.
>
> Provide a facility for users to "time-travel" to previous states of node_modules without having to commit the directory itself.
>
> To facilitate greater visibility of tree changes through readable source control diffs.
>
> And optimize the installation process by allowing npm to skip repeated metadata resolutions for previously-installed packages."

## Edit ##

To answer jrahhali's question below about just using the package.json with exact version numbers. Bear in mind that your package.json contains only your direct dependencies, not the dependencies of your dependencies (sometimes called nested dependencies). This means with the standard package.json you can't control the versions of those nested dependencies, referencing them directly or as peer dependencies won't help as you also don't control the version tolerance that your direct dependencies define for these nested dependencies.

Even if you lock down the versions of your direct dependencies you cannot 100% guarantee that your full dependency tree will be identical every time. Secondly you might want to allow non-breaking changes (based on semantic versioning) of your direct dependencies which gives you even less control of nested dependencies plus you again can't guarantee that your direct dependencies won't at some point break semantic versioning rules themselves.

The solution to all this is the lock file which as described above locks in the versions of the full dependency tree. This allows you to guarantee your dependency tree for other developers or for releases whilst still allowing testing of new dependency versions (direct or indirect) using your standard package.json.

NB. The previous shrink wrap json did pretty much the same thing but the lock file renames it so that it's function is clearer. If there's already a shrink wrap file in the project then this will be used instead of any lock file.
