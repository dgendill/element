# How To Build on Windows

1. Run yarn in project root

2. Run `npm run clean; npm run build:file; npm run lint; npm run webpack -- --config build/webpack.conf.js; npm run webpack -- --config build/webpack.common.js; npm run webpack -- --config build/webpack.component.js; npm run build:utils; npm run build:umd; npm run build:theme`