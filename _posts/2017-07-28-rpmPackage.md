---  
layout: post  
title: rpmPackage
date: 2017-07-28  
categories: blog  
tags: [Java]  
description: rpmPackage 
  
---  
  
======== rpm package =======
1. tree .
		|-- pkgdir
		|   |-- BUILD
		|   |-- RPMS
		|   |-- SOURCES
		|   |-- SRPMS
		|   `-- tmp
		|-- rpmpkgRoot
		|   `-- tmp
		|       `-- test
		|           `-- HNWTest
		|               `-- test
		|                   `-- test.txt
		`-- test.spec
2. test.spec
	#ident	"%W%"
	%define name HNWTest
	%define pkgowner hnwrpt
	%define pkggroup hnwrpt
	%define runowner hnwrpt
	%define rungroup hnwrpt

	Name: %{name}
	Summary: %{name} package
	Version: %{version}
	Vendor: Citigroup
	Packager: US IMACE TEAM
	Release: linux
	Group: Application
	License: None

	# Prefix defines the relocations for a package, i.e. the top level path
	# components you want to place in other locations. The relocation is
	# specified on the install command line like:
	# --relocation /bin=/opt/arbitrary-package/bin
	# The order the prefixes are specified in is important if you are using
	# the relocation information in any of the pre/post install/uninstall scripts
	# or in trigger scripts. The RPM_INSTALL_PREFIX array will be ordered as the
	# prefixes are laid out here (RPM_INSTALL_PREFIX contains the value of the
	# relocations)
	Prefix: /tmp/test/%{name}
	Provides: %{name}
	
	## ignore error: Couldn't exec /usr/lib/rpm/check-files: No such file or directory
	%define _unpackaged_files_terminate_build 0

	%description
	%{name} package

	%pre
	echo Doing preinstall

	%post
	echo "Start postinstall..."

	%postun
	echo "Start post-uninstall..."

	%files
	%dir %attr(0755,%{pkgowner},%{pkggroup}) /tmp/test/%{name}/test
	%attr(0755,%{pkgowner},%{pkggroup})/tmp/test/%{name}/test/*

	%changelog

3. build rpm package (current path : /home/dy83694/test)
	rpmbuild --bb --buildroot=/home/dy83694/test/rpmpkgRoot --define '_topdir /home/dy83694/test/pkgdir/' --define 'version 1.1' --define '_tmppath /home/dy83694/test/pkgdir/tmp/' -vv /home/dy83694/test/test.spec
	tree .
	|-- pkgdir
	|   |-- BUILD
	|   |-- RPMS
	|   |   `-- x86_64
	|   |       `-- HNWTest-1.1-linux.x86_64.rpm
	|   |-- SOURCES
	|   |-- SRPMS
	|   `-- tmp
	|-- rpmpkgRoot
	|   `-- tmp
	|       `-- test
	|           `-- HNWTest
	|               `-- test
	|                   `-- test.txt
	`-- test.spec

