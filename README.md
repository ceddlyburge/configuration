# Configuration

A C# library for strongly typed Configuration with validation

[![Build status](https://ci.appveyor.com/api/projects/status/oujy1v19iwdba8e5?svg=true)](https://ci.appveyor.com/project/RESSoftwareTeam/configuration)

[![Quality Gate](https://sonarcloud.io/api/badges/gate?key=res.configuration)](https://sonarcloud.io/dashboard?id=res.configuration)

[![codecov](https://codecov.io/gh/resgroup/configuration/branch/master/graph/badge.svg)](https://codecov.io/gh/resgroup/configuration)

Example Usage (`Configuration` is the class provided by this repo)

```csharp
public class EconomicModelConfiguration, ICurrencyConversionConfiguration, IConcreteCostConfiguration 
{
    readonly Configuration configuration;
    
    public EconomicModelConfiguration(Configuration configuration) {
        Contract.Requires(configuration != null);

        this.configuration = configuration;
    
        Validate();
    }
    
    void Validate() {
        using (var validator = configuration.CreateValidator) {
            validator.Check(() => DefaultCurrency);
            validator.Check(() => DefaultConcreteCost);
        }
    }

    public string DefaultCurrency => 
        configuration.GetEnum<Currency>(MethodBase.GetCurrentMethod());

    public double DefaultConcreteCost => 
        GetDouble(MethodBase.GetCurrentMethod());
}
```

More details on motivation and  philosophy in [Taming configuration in C#](https://hackernoon.com/taming-configuration-in-c-a2706b2d4741) blog post.
