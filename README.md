# Cube and Hexa — GameBull WebGL (PRODUCTION)

Served by GitHub Pages from `main`, root:
**https://alishehroz-ideo.github.io/cube-and-hexa/**

This is the live URL handed to the GameBull admin panel. **Never push a staging build here.**

No build has been published yet — this repo currently holds only the Pages scaffolding.
To publish one, with Unity closed:

```
Unity.exe -quit -batchmode -nographics -projectPath "<project>" \
  -executeMethod GameBullBuild.SetProductionEnvironment
Unity.exe -quit -batchmode -nographics -buildTarget WebGL -projectPath "<project>" \
  -executeMethod GameBullBuild.BuildProductionBatch
```

Then commit and push the project's `prodbuild/` folder here.

- Environment: **production** — `https://api.g-b.store`
- `.nojekyll` must stay. Without it Pages runs Jekyll, which drops paths beginning with an
  underscore. It lives in this repo and NOT in Unity's output, so check `git status` for
  deletions before committing a rebuilt folder.
- The folder name is load-bearing: Unity names the artifacts after it, so the build must come
  out of a folder called `prodbuild` or `index.html` 404s on its own loader.
