I might make bash versions for my ps profile scripts at some point.

# Initialize a project
This initializes a project in a src root folder under a category then opens the project in vs code insiders

If no category is specified it will automatically place it under a general folder

Usage: `proj-init	git-repo [category]`

This is meant to be added to your Powershell profile.

```PowerShell
function proj-init {
    Param($GitRepo,
        $ProjectName,
        $Category = 'general'
    )
    $Editor = code-insiders
    $SrcPath = 'C:\your-source-directory'
    $FullPath = Join-Path $SrcPath $Category
    $Arguments = @{}
    $Arguments["ArgumentList"] = If ($ProjectName) {"'clone', '$GitRepo', '$ProjectName'"} Else {"'clone', '$GitRepo'"}
    $Arguments["WorkingDirectory"] = $FullPath
    if ( -not (Test-Path -Path $FullPath)) {
        New-Item -Path $SrcPath -Name $Category -ItemType "directory"
    }
    Set-Location $FullPath
    #Start-Process -Wait -Verb open -FilePath "git" @Arguments
	git clone $GitRepo $ProjectName
    $Editor .
}
```

# Installs and starts a yarn project

Usage: Simply run ys inside of a node project's root folder.

This is meant to be added to your Powershell profile

```PowerShell
function ys {
	yarn install
	yarn start
	}
```