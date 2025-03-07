## Gather VODSL files

When working from VODSL representation of a model, the toolkit requies all dependent models to also be available in VODSL format.

*build.gradle.kts:* is expecting to find all VODSL files in ./build/vodsl

The following will populate this directory with models required for the Measurement model.
```
%> mkdir ./build/vodsl 
%> cp ../model/Meas-v1.0.vodsl ./build/vodsl/. 
  Download the appropriate version of vo-dml/XML files from ivoa.net: Coords-v1.0.vo-dml.xml, IVOA-v1.0.vo-dml.xml 
%> gradle vodmlToVodsl --dml=IVOA-v1.0.vo-dml.xml --dsl=build/vodsl/IVOA-v1.0.vodsl 
%> gradle vodmlToVodsl --dml=Coords-v1.0.vo-dml.xml --dsl=build/vodsl/Coords-v1.0.vodsl 
```

## Make model modifications

Edit the model VODSL files to reflect any changes to the model or text descriptions.

## Generate new VO-DML/XML file

```%> gradle vodslToVodml ```

Output file will be written to ./build/generated/vo-dml

## Verify/Modify generated VO-DML/XML file

Check that the model changes are properly reflected in the vo-dml/xml file.  Also, the translation script does not populate
certain fields, and these need to be hand-edited.
* &LTimport&GT nodes: the VODSL import operation does not allow for providing the URL information.
    * &LTurl&GT URL does not include the base 'https://www.ivoa.net/xml/VODML/'
    * &LTdocumentationURL&GT value is not populated.
* &LTconstraint&GT nodes:
    * open question here, the VODSL has the constraints in the text, but as comments.. and they are not transferred
      to the output vo-dml/xml file.

## Replace version controled copy at

```%> cp ./build/generated/vo-dml/Meas-v1.0.vo-dml.xml ../vo-dml/Meas-v1.0.vo-dml.xml ```


## Update model diagrams for PDF documentation

For this project, I've been using Modelio v3.7 for the modeling and diagrams.  With the conversion to VODSL for the model description, I'll still be using Modelio for the diagrams.  This opens potential for discrepancies, but the advantage of having a simple, machine-readable source for the model description outweighs that risk.
There are no details for this, the Modelio .xmi file does not include the diagrams, so short of importing a Modelio Project .zip file, there is no way of loading the current diagram suite.

Replace images at ../doc/diagrams


## Generate new VO-DML/XML file

```%> gradle vodmlDoc```