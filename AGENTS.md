# Project Guidelines

## Purpose

This repository is the Gradle-based template for BoxLang modules that can include both Java and BoxLang code.
Treat it as a template first: preserve placeholders, setup flow, packaging conventions, and generated module structure unless the task explicitly asks to change the template contract.

## Architecture

- Module metadata and runtime lifecycle live in `src/main/bx/ModuleConfig.bx`.
- BoxLang source belongs under `src/main/bx`; Java source belongs under `src/main/java`; tests belong under `src/test`.
- Keep in mind that each BoxLang module is loaded in its own class loader. Avoid changes that assume shared static state, direct classpath leakage, or IDE-only resource loading behavior.
- Custom runtime integrations should follow the existing module folders and registration patterns: `bifs`, `interceptors`, `components` or `tags`, `libs`, and service-loader backed Java types.

## Build And Packaging

- Use the Gradle wrapper from the repo root for build tasks.
- Prefer narrow validation first: `./gradlew test`, `./gradlew spotlessCheck`, or a targeted Gradle task related to the touched area.
- Preserve the packaging pipeline in `build.gradle`: shadow jar output, service loader generation, `build/module` assembly, and zip distribution artifacts.
- Do not reintroduce `src/main/resources` onto the IDE test classpath unless the task explicitly requires it; this template excludes it to avoid BoxLang class loading conflicts during module development.

## Conventions

- Follow `.editorconfig` indentation and line-ending rules. This repo uses tabs by default, with spaces for YAML.
- Follow the Ortus Java formatter in `.ortus-java-style.xml` for Java changes.
- Keep BoxLang module metadata, `box.json`, `settings.gradle`, and Gradle properties aligned when changing names, versions, or packaging identifiers.
- Prefer small template-safe edits. If a change would affect generated modules, update both the implementation and any setup or template placeholders that keep the template consistent.

## Skills

- Relevant BoxLang development skills live under `.agents/skills`. Use them when the task involves module development, BIFs, components, interceptors, logging, async tasks, or runtime architecture.
- When a task is specifically about custom instructions, prompts, agents, or skills, prefer the agent-customization workflow and keep AGENTS.md focused on workspace-wide rules only.
