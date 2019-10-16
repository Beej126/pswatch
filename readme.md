This powershell cmdlet continuously monitors a directory tree and write to the output the path of the file that has changed.

This allows you to create an script that for instance, run a suite of unit tests when an specific file has changed using powershell pipelining.

Installation
============

Download the psm1 file in My documents\WindowsPowershell\Modules\pswatch or simply run this one line installation script:

	iex ((new-object net.webclient).DownloadString("https://raw.githubusercontent.com/Beej126/pswatch/master/install.ps1"))

Usage
=====

A simple example will be:

	Import-Module pswatch

	watch "Myfolder\Other" | %{
		Write-Host "$_.Path has changed!"
		RunUnitTests.exe $_.Path
	}

You can filter by using powershell pipelining as follows:

	watch | Get-Item | Where-Object { $_.Extension -eq ".js" } | %{
		do the magic...
	}

Options
=======

The watch cmdlet has the following parameters:

  * location: file or folder to watch. (required)
