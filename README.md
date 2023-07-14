# SEICT - COMPRAC - Open Api Spec

## Getting started

### Tooling

- VS Code - [Download](https://code.visualstudio.com/sha/download?build=stable&os=win32-x64)
- Java 17+ - [Download Page](https://www.oracle.com/java/technologies/downloads/)
- Maven - [Download Page](https://maven.apache.org/download.cgi)
- Prism - [Installation Page](https://docs.stoplight.io/docs/prism/f51bcc80a02db-installation)

> Remember to set environment vars JAVA_HOME and MVN_HOME 

> Remember to add JAVA_HOME and MVN_HOME to 

### Plugins

- [Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph)
- [Open Api Editor](https://marketplace.visualstudio.com/items?itemName=42Crunch.vscode-openapi)
- [Open Api Linter](https://marketplace.visualstudio.com/items?itemName=stoplight.spectral)
- [SonarLint](https://marketplace.visualstudio.com/items?itemName=SonarSource.sonarlint-vscode)

## Open API - Dev Flow

- [OAS Dev Docs](https://swagger.io/docs/specification/about/) - Bookmark it. now. do it.
- Develop spec file on:
    > src\main\resources\openapi\spec\specFile_oas3.yml
- Run the codegen on local
    > mvn clean compile
- Check Back End files generated at:
    > target\generated-sources\openapi\src
    - api: Contains the Endpoints Services classes.
    - model: Contains the Api classes (request|response|etc).
- Check Front End files generated 
    > src\main\resources\openapi\generated\fe\lib-client
    - api: Contains the Endpoints Services classes.
    - model: Contains the Api classes (request|response|etc).
    - README.md: Contains Instructions on how to setup the Api module.
- If files are ok and maven returns a sucess => OK.

### Modify the Codegen

- [Open Api Generators - List](https://openapi-generator.tech/docs/generators)
- [Backend - Spring Generator](https://openapi-generator.tech/docs/generators/spring)
- [Frontend - Typescript Angular Generator](https://openapi-generator.tech/docs/generators/typescript-angular)
- Codegen is configured to run by Maven, so check the `pom.xml` file.
- Edit section `<properties>` - properties have prefixes that help understanding them, form example: `.*codegen.be.*` relates to backend.
- Plug the edited properties in the respective `<execution>` that generates the type of artefact you edited.
- Run codegen again.

## Open Api - Mock Server

- [Prism](https://stoplight.io/open-source/prism) allows us to start a server locally that can serve responses and examples based on the spec file, faking a backend server.
- Install prism 
    > npm install -g @stoplight/prism-cli
- Open a terminal and go to the root of project
- Start mock server
    > prism mock -d .\src\main\resources\openapi\spec\${spec_file_name_here}.yml
- Customize your app environment to use the api url
    > http://localhost:4010

### Dynamic Mocked Responses

- [Open Api How to Add Examples](https://swagger.io/docs/specification/adding-examples/)
- [Prism Dynamic Mocks](https://docs.stoplight.io/docs/prism/83dbbd75532cf-http-mocking)
- [Prism Dynamic Response Generation](https://docs.stoplight.io/docs/prism/9528b5a8272c0-dynamic-response-generation-with-faker)
- Add example and alias on the spec (read above on how to)
- Add the example alias as a preference of your request to the mock server
    > Prefer:example=${yourExampleAlias}
     