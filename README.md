CuiSantafesino
==============

This is my version of the original work of Juan Vuletich http://www.jvuletich.org/Cuis/Index.html

I create the sources using

'From Cuis 3.1 of 4 March 2011 [latest update: #850] on 4 October 2014 at 8:15:49 am'!

!Object methodsFor: 'sources managment' stamp: 'edc 2/12/2008 07:43'!
createDirIfnotExists: aDirName
(FileDirectory default directoryExists:aDirName)
		ifFalse: [FileDirectory default createDirectory: aDirName].
	^FileDirectory default directoryNamed: aDirName! !

!Object methodsFor: 'sources managment' stamp: 'edc 10/4/2014 02:32'!
createSources
" Object new createSources"
| unzipped nameToUse zipped dir |
ProtoObject allSubclassesWithLevelDo:[:cl :l| 
	dir := self createDirIfnotExists:cl category asString.
	
	
	Cursor write showWhile: [nameToUse :=  cl printString, FileDirectory dot,'.st'  .
		(dir fileExists: nameToUse) ifFalse:[
			unzipped :=RWBinaryOrTextStream on: ''.
			unzipped header; timeStamp.
	 cl  fileOutOn: unzipped moveSource: false toFile: 0.
	unzipped trailer.
	
			unzipped reset.
			zipped := dir newFileNamed: nameToUse.
	
			zipped close.
			unzipped close]]] startingLevel: 0! !
