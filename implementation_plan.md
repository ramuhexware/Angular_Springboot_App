# Implementation Plan - Fix & Polish Spring Boot + Angular 17 CRUD Project

The workspace contains a Spring Boot + Angular 17 CRUD application project. Upon auditing the workspace, several critical missing components and incomplete code structures were identified:

1. **Missing Angular Components**: `app.module.ts` and `app-routing.module.ts` import `TutorialsListComponent` and `TutorialDetailsComponent`, but their corresponding source files (`.ts`, `.html`, `.css`) in `angular-17-client/src/app/components/` are missing, which breaks the Angular build.
2. **Missing Spring Boot Java Files**: `spring-boot-server` has `pom.xml` and configuration, but the Java package `com.bezkoder.spring.jpa.h2` is missing all implementation classes: the main `@SpringBootApplication` entry point, the `@Entity` model (`Tutorial`), the `TutorialRepository` interface, and the `TutorialController` REST controller.
3. **Project Cleanup**: Audit and remove any empty directories, orphan files, or misconfigurations to ensure a clean, production-ready codebase.

---

## User Review Required

> [!IMPORTANT]
> - **Missing Backend Java Code**: The backend was missing its entire source code layer (Application, Model, Repository, Controller). We will create standard Spring Boot REST API classes that pair with the Angular 17 CRUD frontend.
> - **Missing Frontend Components**: The frontend had routing and module declarations for `TutorialsListComponent` and `TutorialDetailsComponent`, but their directory contents were empty. We will implement both components fully.

---

## Proposed Changes

### Spring Boot Backend (`spring-boot-server`)

#### [NEW] [SpringBootJpaH2Application.java](file:///c:/ramu/Project_Assignment/RapidX/FreddeMac_Project_RapidX/Work/Simple_Projects/Angular_project/spring-boot-server/src/main/java/com/bezkoder/spring/jpa/h2/SpringBootJpaH2Application.java)
- Main class annotated with `@SpringBootApplication` to boot the server on port 8080.

#### [NEW] [Tutorial.java](file:///c:/ramu/Project_Assignment/RapidX/FreddeMac_Project_RapidX/Work/Simple_Projects/Angular_project/spring-boot-server/src/main/java/com/bezkoder/spring/jpa/h2/model/Tutorial.java)
- `@Entity` mapping `id`, `title`, `description`, and `published` attributes with getters, setters, and constructors.

#### [NEW] [TutorialRepository.java](file:///c:/ramu/Project_Assignment/RapidX/FreddeMac_Project_RapidX/Work/Simple_Projects/Angular_project/spring-boot-server/src/main/java/com/bezkoder/spring/jpa/h2/repository/TutorialRepository.java)
- Extends `JpaRepository<Tutorial, Long>` with `findByPublished(boolean published)` and `findByTitleContaining(String title)`.

#### [NEW] [TutorialController.java](file:///c:/ramu/Project_Assignment/RapidX/FreddeMac_Project_RapidX/Work/Simple_Projects/Angular_project/spring-boot-server/src/main/java/com/bezkoder/spring/jpa/h2/controller/TutorialController.java)
- `@CrossOrigin(origins = "http://localhost:8081")` REST controller implementing CRUD operations (`/api/tutorials`).

---

### Angular 17 Frontend (`angular-17-client`)

#### [NEW] [tutorials-list.component.ts](file:///c:/ramu/Project_Assignment/RapidX/FreddeMac_Project_RapidX/Work/Simple_Projects/Angular_project/angular-17-client/src/app/components/tutorials-list/tutorials-list.component.ts)
#### [NEW] [tutorials-list.component.html](file:///c:/ramu/Project_Assignment/RapidX/FreddeMac_Project_RapidX/Work/Simple_Projects/Angular_project/angular-17-client/src/app/components/tutorials-list/tutorials-list.component.html)
#### [NEW] [tutorials-list.component.css](file:///c:/ramu/Project_Assignment/RapidX/FreddeMac_Project_RapidX/Work/Simple_Projects/Angular_project/angular-17-client/src/app/components/tutorials-list/tutorials-list.component.css)
- Component to view all tutorials, search by title, select a tutorial to view details, and remove all tutorials.

#### [NEW] [tutorial-details.component.ts](file:///c:/ramu/Project_Assignment/RapidX/FreddeMac_Project_RapidX/Work/Simple_Projects/Angular_project/angular-17-client/src/app/components/tutorial-details/tutorial-details.component.ts)
#### [NEW] [tutorial-details.component.html](file:///c:/ramu/Project_Assignment/RapidX/FreddeMac_Project_RapidX/Work/Simple_Projects/Angular_project/angular-17-client/src/app/components/tutorial-details/tutorial-details.component.html)
#### [NEW] [tutorial-details.component.css](file:///c:/ramu/Project_Assignment/RapidX/FreddeMac_Project_RapidX/Work/Simple_Projects/Angular_project/angular-17-client/src/app/components/tutorial-details/tutorial-details.component.css)
- Component to edit, publish/unpublish, and delete a specific tutorial.

#### Cleanup & Verification
- Clean up any stray temporary files or broken empty directories.
- Verify Angular compilation build (`npm run build` or `ng build`).
- Verify Maven build (`mvn clean compile`).

---

## Verification Plan

### Automated Tests
- Run `mvn test-compile` or `mvn compile` inside `spring-boot-server` to verify Java code compiles without errors.
- Run `npm run build` inside `angular-17-client` to verify Angular app builds cleanly without missing import or syntax errors.

### Manual Verification
- Review generated file paths and check for any remaining missing components.
