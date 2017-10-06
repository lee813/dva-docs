## Code Structure Design

When we are scaffolding our project, we always ignore how to organize our code structre. In fact, a clean code structure will always provide us a clean standard to scaffold our project.
In dva project, we recommend the basic structure as follows:

```bash
.
├── /mock/           # mock interface
├── /src/            # source code of project
│ ├── /components/   # components
│ ├── /routes/       # route components (page based)
│ ├── /models/       # data model
│ ├── /services/     # data interface
│ ├── /utils/        # utilities
│ ├── route.js       # route configuration
│ ├── index.js       # entry point
│ ├── index.less     
│ └── index.html     
├── package.json     # project info
└── proxy.config.js  # mock configuration
```

We can find that dva maps all the possible functionalities to the folder respectively, in addition, we have a clean view for all the functionalitiesof our project, so we recommend that you can follow this structure to organize your code. If you are using dva-cli to building the dva template, it can help generate this structure automatically.


Next [Design Model](./03_design_model.md)。
