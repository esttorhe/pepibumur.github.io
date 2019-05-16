---
title: The hermeticism and rigidity of Xcode and its projects
excerpt: Xcode and its projects are not as flexible as they could be, which makes it hard for companies to optimize their workflows and processes. In this post I'll analyze some of the things that I would improve from its build system and projects.
tags: [hooked, internet, products]
---

If you work with Xcode you are most likely familiar with its hermeticism. Compared to other programming languages, like Kotlin, where the build system is independent of the IDE *(Gradle)*, in Xcode everything is together and not well documented. Xcode projects have build settings and build phases that are the input to the build system that Xcode uses. Have you ever searched for what each of the build settings means? You'll most likely end up on StackOverflow or some random website where someone tried to figure out what these settings are for. Documentation is terrible, and developers have to do some reverse engineering to understand what they are for. When I see other build systems like Gradle, where you have total flexibility during the build process, and everything is documented I feel jealous. I wish Apple had something like that with Xcode. I'm optimistic, and I believe it's going to happen sooner or later, but I think we are far from having it.

Besides the hermeticism of the build system, another thing that annoys me is its rigidness. Build settings and build phases is the only input, and they are very static, you can't do much with them. For example, if you want to link a library/framework when some conditions are met you cannot. You need to write your scripts that can be hooked from Xcode build phases but they cannot participate in the build of the source code. Only build settings, and sources buidl phases can determine what and how needs to be built. If you add a custom build phase that links a library conditionally, then it breaks the scheme *"Find implicit dependencies"* because Xcode is not aware of your custom linking. Bad, isn't it?

Although this works for most of the projects, as soon as you need to optimize things in the way your project is built, then you are fucked. Companies like Pinterest, Uber, or Facebook has moved to other build systems like Bazel and Buck. Besides the powerful features that they get from them, they are very flexible, especially Bazel, so you can customize any step of your project build. One important difference between Buck and Bazel for instance is that Bazel allows you to define custom phases using a programming language similar to Python. For companies like Shopify, where there a lot of engineers building the app every day, where our CI infrastructure is compiling every commit that is sent to the git repository, it's essential that we have a fair amount of flexibility. We'll work soon on having incremental builds on CI. The idea is to dynamically share build artifacts across the pipeline builds, copying only the artifacts that are necessary for Xcode not to compile the frameworks/libraries that don't need to be compiled. To do that, you need to know how Xcode manages the derived data directory, how the build system turns the input *(build settings, build phases, source files, and resources)* into intermediate and final artifacts. Does Xcode use the file update date to determine what needs to be built? Is it necessary to copy the intermediate files if there are some final ones? Well, we don't know. With Bazel and Buck, not only they know about what output is generated from some given input, but also you know.

Another rigid component of Xcode is its projects. When a company has a few Xcode projects to maintain, it's important to be consistent and share as much as possible across all the projects. It makes maintenance easier. Someone might argue that sharing is possible using .xcconfig files, and it's true, but partially. .xcconfig files allow you to reuse build settings, but if you want to reuse build phases, targets or schemes structure, then you cannot. We have a few modules at Shopify that are shared across all the company iOS applications. They have similar build settings, same targets and schemes structure, but they are not sharing anything. If we want to update the deployment target or add a new target in each of them, we have to go one by one updating it manually. While this is something we can do when there are 4/5 modules, it becomes a pain in the ass when there are 10 or 20. It's easy to forget something, and suddenly the project doesn't compile. [XcodeGen](https://github.com/yonaskolb/XcodeGen) is an open source tool that helps you overcome this issue. Projects are defined in yaml, so you can use all reusing options that the yaml format offers. It also provides a more flexible way to define and share your build settings. I've used it to describe a [modular app](https://github.com/pepibumur/xcode-modular-apps-workshop) that I'll build in the workshop that I'm giving at [Mobos](http://romobos.com/), and I was able to have a repository with no Xcode project in it, and sharing configuration across all modules that are part of the project. Wouldn't it be great if Apple followed a similar approach and provided something similar? Imagine something like the SPM `Package.swift` but for apps projects, `Project.swift`. 

As I said, I'm optimistic. Apple open sourced Swift, and is open sourcing components of the Xcode and its build system. Not sure if having it open source will make it more flexible, but at least there will be an open space where we'll be able to participate in discussions about the future of the build system. Software engineers will be able to bring ideas to the Xcode build system, and other build systems will be able to take some from Apple's one.