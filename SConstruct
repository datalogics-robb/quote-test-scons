# -*- Python -*-
import os
import glob
import SCons.Util


env = Environment()
samples_manifest = set()
csproj_files = set()
samples = []
CSPROJ_CONTENTS = ('''
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
    <Platforms>x64;ARM64</Platforms>
    <AppendTargetFrameworkToOutputPath>false</AppendTargetFrameworkToOutputPath>
  </PropertyGroup>

  <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Debug|x64'">
    <OutputPath>..\..\..\Binaries</OutputPath>
  </PropertyGroup>
  <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Debug|ARM64'">
    <OutputPath>..\..\..\Binaries</OutputPath>
  </PropertyGroup>
  <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|x64'">
    <OutputPath>..\..\..\Binaries</OutputPath>
  </PropertyGroup>
  <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|ARM64'">
    <OutputPath>..\..\..\Binaries</OutputPath>
  </PropertyGroup>
  <ItemGroup>
    <Reference Include="Datalogics.PDFL">
      <HintPath>..\..\..\@HINT_PATH@\Datalogics.PDFL.dll</HintPath>
    </Reference>
  </ItemGroup>

</Project>
''')

# Because we do not want to build the samples in the dist directory (they would get shipped)
# and we do not want to copy the entire dist directory for .NET Core, just to build samples,
# We point the csproj files to a different path for
# For distribution we need this @HINT_PATH@: <HintPath>..\..\..\Binaries\Datalogics.PDFL.dll</HintPath>
# For testing, we need this @HINT_PATH@:  <HintPath>..\..\..\NETCore\bin\$(Platform)\$(Configuration)\Datalogics.PDFL.dll</HintPath>

testproj = env.Textfile(target='GenFile.csproj',
                        source=CSPROJ_CONTENTS,
                        SUBST_DICT={'@HINT_PATH@': r'NETCore\bin\$($Platform$)\$($Configuration$)'})
