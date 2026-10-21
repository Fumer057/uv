# What I Learned

## Making `uv run hello-world` work

### What went wrong

I tried to run `uv run hello-world`, but the project did not initially define a command named `hello-world`. After adding the command in `pyproject.toml`, the build still failed because the project was missing the Python package file in the location expected by `uv_build`.

### How I fixed it

I added this script entry to `pyproject.toml`:

```toml
[project.scripts]
hello-world = "hello_world:main"
```

Then I put the `main()` function in `src/hello_world/__init__.py`. The script entry points to the `main` function in the `hello_world` package, and that file is in the folder structure expected by the build system.

After that, `uv run hello-world` worked and printed `Hello from hello-world!`.
