# Publishing a package

uv does not yet have dedicated commands for building and publishing a package. Instead, you can use
the PyPA tools [`build`](https://github.com/pypa/build) and
[`twine`](https://github.com/pypa/twine), both of which can be invoked via `uvx`.

## Preparing your project for packaging

Before attempting to publish your project, you'll want to make sure it's ready to be packaged for
distribution.

If your project does not include a `[build-system]` definition in the `pyproject.toml`, uv will not
build it by default. This means that your project may not be ready for distribution. Read more about
the effect of declaring a build system in the
[project concept](../concepts/projects.md#build-systems) documentation.

## Building your package

Build your package with the official `build` frontend:

```console
$ uvx --from build pyproject-build --installer uv
```

!!! note

    Using `--installer uv` is not required, but uses uv instead of the default, pip, for faster
    builds.

The build artifacts will be placed in `dist/`.

## Publishing your package

Publish your package with `twine`:

```console
$ uvx twine upload dist/*
```

!!! tip

    To provide credentials, use the `TWINE_USERNAME` and `TWINE_PASSWORD` environment variables.

## Installing your package

Test that the package can be installed and imported with `uv run`:

```console
$ uv run --with <PACKAGE> --no-project -- python -c "import <PACKAGE>"
```

The `--no-project` flag is used to avoid installing the package from your local project directory.

!!! tip

    If you have recently installed the package, you may need to include the
    `--refresh-package <PACKAGE>` option to avoid using a cached version of the package.

## Next steps

To learn more about publishing packages, check out the
[PyPA guides](https://packaging.python.org/en/latest/guides/section-build-and-publish/) on building
and publishing.

Or, read on for more details about the concepts in uv.
