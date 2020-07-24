This topic covers how to use LibMan in a continuous integration build.

Ideally you will want to set some variables for all your projects. The easiest way to do this is to add the following to a [Directory.Build.props](https://docs.microsoft.com/en-us/visualstudio/msbuild/customize-your-build?view=vs-2019#directorybuildprops-and-directorybuildtargets) next to your solution file.

```
<Project>
	<PropertyGroup>
		<RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
		<RestoreLockedMode Condition="'$(IsContinuousIntegrationBuild)' == 'true'">true</RestoreLockedMode>
	</PropertyGroup>
	
	<ItemGroup>
		<SourceRoot Include="$(MSBuildThisFileDirectory)" />
	</ItemGroup>
</Project>
```

You will need to pass a `ContinuousIntegrationBuild` MSBuild variable *or* you can set an environment variable before running the build.

An example of passing the MSBuild variable looks like this:

```
dotnet build /p:IsContinuousIntegrationBuild=true
```

Additional Notes
===
Azure Pipelines
---
Azure pipelines exposes the `TF_BUILD` environment variable.

It is possible to cache the libman cache between runs to save some build time, the following should be added to the `.yml` file for the hosted ubuntu image

```
variables:
  libman_packages: /home/vsts/.local/share/.librarymanager/cache
 
steps:
  - task: Cache@2
    inputs:
      key: 'libman | "$(Agent.OS)" | **/libman.json,!**/bin/**,!**/artifacts/**'
      path: $(libman_packages)
    displayName: Cache Libman packages
```