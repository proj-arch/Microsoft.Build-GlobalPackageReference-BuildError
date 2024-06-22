# Microsoft.Build-GlobalPackageReference-BuildError
Demonstrates the error that occurs when adding Microsoft.Build as GlobalPackageReference instead of a direct PackageReference.

Issue https://github.com/dotnet/msbuild/issues/10281

### Description
Using the package __Microsoft.Build__ as __GlobalPackageReference__ doesn't really import the contained assembly.  
For example using Microsoft.Build.Evaluation.Project like this...

    public class Class1
    {
        public void UseMicrosoftBuildEvaluationProject()
        {
            var project = new Microsoft.Build.Evaluation.Project("SomeProject.csproj");
        }
    }

... leads to this error:

    CS0234: The type or namespace name 'Build' does not exist in the namespace 'Microsoft' (are you missing an assembly reference?)

But specifying the PackageVersion only in Directory.Package.props and adding a PackageReference to the Directory.Build.props is working fine. 

### Steps
1. clone the repo
2. build GlobalPackageReference-BuildError\GlobalPackageReference-BuildError.sln
3. you will get the error

but on the other hand this works:

1. clone the repo
2. build GlobalPackageReference-Working\GlobalPackageReference-Working.sln
3. this builds fine