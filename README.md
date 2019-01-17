# Configuration

A C# library for strongly typed Configuration with validation

[![Build status](https://ci.appveyor.com/api/projects/status/gonvdsbebdla0sxo?svg=true)](https://ci.appveyor.com/project/ceddlyburge/configuration)

[![Quality gate](https://sonarcloud.io/api/project_badges/quality_gate?project=ceddlyburge_configuration)](https://sonarcloud.io/dashboard?id=ceddlyburge_configuration)

[![codecov](https://codecov.io/gh/ceddlyburge/configuration/branch/master/graph/badge.svg)](https://codecov.io/gh/ceddlyburge/configuration)

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
        configuration.GetDouble(MethodBase.GetCurrentMethod());
}
```
More details on motivation and  philosophy in [Taming configuration in C#](https://hackernoon.com/taming-configuration-in-c-a2706b2d4741) blog post.

Nuget package available at https://www.nuget.org/packages/RES.Configuration/
