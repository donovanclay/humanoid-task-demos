# Humanoid Task Demos

Static viewer for the Molmobot humanoid (Unitree G1, Dex3 hands) task demos: third-person and robot cameras per clip, grouped by task. Served by GitHub Pages from `main` (root) at https://donovanclay.com/humanoid-task-demos/ (the account's custom domain; `donovanclay.github.io/humanoid-task-demos/` redirects there). Open `index.html` through a web server to view locally.

## Layout

- `index.html`: the page. It fetches `data.json`.
- `data.json`: list of tasks, each with `id`, `family`, `title`, `description` and `clips` (`src` = third-person clip, optional `robot` = robot-camera clip, `caption`, `meta`).
- `v/<task>/NN.mp4` and `NN_robot.mp4`: the clips.
- `.nojekyll`: Pages serves the files as is.

## Updating

The content is a copy of the staged `site/` folder that the task-demos build writes (`build.py` in the owning session's scratchpad, source clips under `$FD_RUNS_DIR/taskdemos_*` and `artopen/`). To update, sync that folder in and push:

    rsync -a --delete --exclude .git --exclude README.md --exclude .nojekyll <site>/ .
    git add -A && git commit -m "Update demos" && git push origin main

Check before pushing that every `src` and `robot` path in `data.json` exists and that no local paths (`/weka`, user names) appear. Keep the whole site under 1 GB (Pages limit) and each file under 100 MB.

If a Pages build hangs in "syncing files" and times out (about 10 minutes), push an empty commit or `gh api -X POST repos/donovanclay/humanoid-task-demos/pages/builds`.
