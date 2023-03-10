
## fixed
> fixed org.eclipse.aether.util.version.GenericVersionScheme#parseVersionConstraint() of module maven-resolver-impl

```
VersionConstraint result;
if ( ranges.isEmpty() )
{
    result = new GenericVersionConstraint( parseVersion( constraint ) );
}
else
{
    VersionRange range = UnionVersionRange.from( ranges ) ;
    boolean upEqLow = range.getLowerBound()!=null&&range.getLowerBound().equals(range.getUpperBound());
    String version = range.getLowerBound().getVersion().toString();
    if(upEqLow && !RELEASE.equals(version) && !LATEST.equals(version) && !SNAPSHOT.equals(version)){
        result = new GenericVersionConstraint(range.getLowerBound().getVersion());
    }else {
        result = new GenericVersionConstraint(range);
    }
}

return result;
```

after fixed will do version `[1.0.0]` the same as `1.0.0`

## package
```
mvn clean package -Drat.skip=true -Dcheckstyle.skip=true
```