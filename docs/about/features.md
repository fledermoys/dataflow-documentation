# Features

Dataflow empowers Adobe After Effects users with a robust suite of tools to streamline data-driven video production. From seamless data integration to advanced automation, the extension is designed to enhance efficiency, flexibility, and creativity for both individual creators and professional teams.

## General Features
- **Seamless Data Connectivity**: Effortlessly connect to local data sources in ==.tsv== or ==.json== formats, or integrate with ==Google Sheets== using a free, user-generated API key from your Google Cloud Project. The comprehensive [setup guide](../documentation/google-api.md) ensures a quick and straightforward configuration process.
- **Real-Time Data Previews**: Visualize data and footage variations within the extension before rendering, enabling precise adjustments and confident project setup.
- **Unlimited Batch Rendering**: Generate countless video versions in a single workflow by injecting data and footage into your After Effects projects, saving time and ensuring consistency across outputs.
- **Customizable User Presets**: Create and save user presets within the extension, allowing rapid selection of project-specific settings.
- **Flexible Render Settings**: Define render settings and output modules for each job, by [defining them in your data source.](../documentation/data-sources.md/##-Dataflow-Columns)
- **Destination Control**: Specify custom output names and destinations per render job, streamlining file organization and delivery.
- **Target Composition**: Wanna render different compositions form the same Project? Just define the target composition in your data source, allowing you to render any composition from your project.
- **Project Switching**: Seamlessly switch between After Effects projects within the same data source by [defining the .aep project file](../documentation/data-sources.md/##-Dataflow-Columns) in your data source, maximizing workflow efficiency.

## Agent Features
- **Automated Rendering with Agent Mode**: Activate Agent Mode to continuously monitor connected data sources for render-ready jobs, defined by the render-status in your data source, providing a hands-off, always-on rendering solution.
- **Multi-Source Monitoring**: Simultaneously watch multiple local data sources or multiple worksheets within a Google Sheet, enabling a single machine to handle rendering for multiple campaigns with distinct data inputs.
- **Scalable Campaign Management**: Leverage Agent Mode’s flexibility to support complex, multi-campaign workflows, ensuring efficient asset production across diverse projects without manual intervention.