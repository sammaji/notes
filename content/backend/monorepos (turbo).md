source: https://turbo.build/repo/docs
## build system 
tools that performs tasks like minifying, linting, building code.
## build system orchestrator
tools that orchestrate the build process. e.g. turborepo, vite.

turborepo is not exactly a mono repo frame work. it orchestrates the build process, so its a build system orchestrator.
## monorepo
a monorepo framework provides tools and conventions for managing projects that contain multiple packages or applications within a single repository (monorepo). This includes dependency management between packages, workspace configuration.

e.g., lerna, nx, yarn workspaces, etc.

## benefits of turborepo
- remote caching
- parallelisation
- dependency graph awareness
## workspace

They are made so that you can share packages in a workspace.

To create a workspace you have to a `pnpm-workspace.yml` file and specify the workspaces.

```yaml
# make docs and everything inside
# packages and app part of workspace.
docs
packages/*
apps/*
```

Each package / app has a name mentioned in the `package.json`.

Package managers uses the name to figure out where to install a package -> `pnpm add react --filter package-name`. You don't need to re-install every time your source code changes inside a package - only when you change the locations (or configuration) of your workspace in some way.

It is also the name of the package (for using locally and publishing to npm).

To use a workspace inside another workspace, you need to specify it as a dependency.

```json
{
	"dependencies": {
		"shared-package": "workspace:*"
	}
}
```

Here, `*` means the latest version, which saves us from needing to bump the versions of our dependency if the versions of our packages change. You can use a specific version too.

## Tasks
Schema ->  `https://turbo.build/schema.json`

In `turbo.json`, we can specify tasks to run. `cache` property configures caching. Making a task `persistent` will allow it to run in the background.

```json
{ "pipeline": { "dev": { "cache": false, "persistent": true } }}
```

`outputs` options takes an array of strings containing paths that are generated as a result of building an application. Turbo uses it to keep track of what to rebuild so that it doesn't build the same thing again.

If a task depends on other tasks, we can mention it.
```json
{
  "pipeline": {
    "dev": {
      "dependsOn": ["codegen", "db:migrate"],
      "cache": false
    },
    "codegen": {
      "outputs": ["./codegen-outputs/**"]
    },
    "db:migrate": {
      "cache": false
    }
  }
}
```

Run a task -> `turbo run <taskname>`
Run a task only targeting a specific workspace -> `turbo run <taskname> --filter <workspace>`

Here's an example of building a next.js app:
```json
{
  "pipeline": {
    "build": {
      "outputs": [".next/**", "!.next/cache/**"]
    }
  }
}
```

## Caching
For every task, you can set `cache` property to true or false. By default, turbo will cache a task.

For the caching to work properly, we need to specify the build outputs, otherwise it will only cache terminal outputs. Basically, turbo keeps track of the inputs (your code) and outputs (your build outputs and terminal outputs). If the inputs changes, then only it will re-run a task, otherwise, it will just use the cached results.

`--no-cache` -> does not cache the outputs of a task.
`--force` -> ignore any cached results, but it will still cache the results.