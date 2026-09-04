# Cube and Hexa — GameBull WebGL (PRODUCTION)

Served by GitHub Pages from `main`, root:
**https://alishehroz-ideo.github.io/cube-and-hexa/**

This is the live URL handed to the GameBull admin panel. **Never push a staging build here** —
staging lives at `alishehroz-ideo/cube-and-hexa-staging`.

This repo holds a Unity WebGL **build output**, not source. Source lives in the Unity project;
a build overwrites `Build/`, `TemplateData/` and `index.html` here.

To publish a new build, with Unity closed (it holds an exclusive lock on the project). The two
steps are separate invocations on purpose: changing a scripting define needs a recompile, and a
build in the same run would still use the old one.

```
Unity.exe -quit -batchmode -nographics -projectPath "<project>" \
  -executeMethod GameBullBuild.SetProductionEnvironment
Unity.exe -quit -batchmode -nographics -buildTarget WebGL -projectPath "<project>" \
  -executeMethod GameBullBuild.BuildProductionBatch
```

- Environment: **production** — `https://api.g-b.store`. The switch sets both the C#
  `GAMEBULL_PRODUCTION` define and the template's own `DEFAULT_API_BASE` and `BUILD_ENV`, so the
  game cannot talk to one environment while the loading icon queries the other.
- Compression: Brotli with the JS decompression fallback, so it works on a plain static host
  that sends no `Content-Encoding` header. ~28 MB transfer.
- `.nojekyll` must stay. Without it Pages runs Jekyll, which drops paths beginning with an
  underscore. It lives in this repo and NOT in Unity's output, so check `git status` for
  deletions before committing a rebuilt folder.
- The folder name is load-bearing: Unity names the artifacts after it, so the build must come
  out of a folder called `prodbuild` or `index.html` 404s on its own loader.

Which build is live: open the console and read the `[Cube and Hexa] build … (production)` line.
Hard-refresh in a private window — a cached wasm makes that question come up constantly.
