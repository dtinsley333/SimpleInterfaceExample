# Simple Interface Example
Most basic interface example. The purpose of this app it to clearly show how an interface works. 

###Interface Created (Contract for classes that will implement it)
```
 public interface ICanine
    {
        string SpeciesName { get; set; }  //example-the scientific name for dog is Canis lupus familiaris
        string CommonName { get; set; }//dog, coyote, wolf, dingo
        bool IsDomestic { get; set; }
        bool IsEndangered { get; set; }
        int GestationDays { get; set; }
        string CoatColor { get; set; }
        string Diet { get; set; }
        int AverageWeight { get; set; }
        int AverageLifeSpan { get; set; }
        string GetHabitatBasedOnCountry(string country);
        int? GetPopulationBasedOnCountry(string country);  //made nullable since code needs to be able to handle unfound country code, country codes frequently change.
    }
}


```

###Class that implements ICanine
```
   class Wolf : ICanine
    {
        public int AverageLifeSpan { get; set; }
        public int AverageWeight { get; set; }
        public int GestationDays { get; set; }
        public string CoatColor { get; set; }
        public string CommonName { get; set; }
        public bool IsDomestic { get; set; }
        public string Diet { get; set; }
        public bool IsEndangered { get; set; }
        public string SpeciesName { get; set; }

        public string GetHabitatBasedOnCountry(string country)
        {
            if (country.Contains("United States") || country.Contains("Canada"))
            {
                return "diverse range of environments, including tundra, mountain areas, woodlands, forests, grasslands and deserts.";
            }

            return "Habitat Unknown";
        }

        public int? GetPopulationBasedOnCountry(string country)
        {
            switch (country)
            {
                case "Australia":
                    return 0;
                case "United States, Canada":
                    return 6663234;
                case "Canada":
                    return 6663234;
                default:
                    return null;
            }
        }
   
```
###Canine classes instanciated using the ICanine interface. This iterface enforced how the specific canine objects are to be used. 

```
 static void Main(string[] args)
        {
            Dog dog = new Dog
            {
                GestationDays = 60,
                AverageLifeSpan = 13,
                AverageWeight = 35,
                CoatColor = "Varies",
                CommonName = "Dog",
                Diet = "Dog food and purloined snacks",
                IsDomestic = true,
                IsEndangered=false,
                SpeciesName= "Canis lupus familiaris"
    };

            Wolf wolf = new Wolf
            {
                GestationDays = 60,
                AverageLifeSpan = 13,
                AverageWeight = 60,
                CoatColor = "Varies",
                CommonName = "Wolf",
                Diet = "Other wildlife",
                IsDomestic = false,
                IsEndangered = false,
                SpeciesName = "Canis lupus"
            };

            //display wolf info
            Console.Write("WOLF INFORMATION" + "\n");
            var wolfCountry = "United States, Canada";
            var wolfPopulation = wolf.GetPopulationBasedOnCountry(wolfCountry);
            var wolfHabitat = wolf.GetHabitatBasedOnCountry(wolfCountry);
            Console.Write("Population for wolves is " + wolfPopulation + " in " + wolfCountry + "\n");
            Console.Write("Habitat for wolves is " + wolfHabitat + " in " + wolfCountry + "\n");
            Console.Write("The scientific name for a wolf is " + wolf.SpeciesName);
            Console.Write("Wolves like to eat " + wolf.Diet + "\n");
           //TODO: Refactor the concatenation spaghetti

            //display dog info
            Console.Write("DOG INFORMATION" + "\n");
            var dogCountry = "United States";
            var dogPopulation = dog.GetPopulationBasedOnCountry(dogCountry);
            var dogHabitat = dog.GetHabitatBasedOnCountry(dogCountry);
            Console.Write("Population for dogs is " + dogPopulation + " in " + dogCountry + "\n");
            Console.Write("Habitat for dogs is " + dogHabitat + " in " + dogCountry + "\n");
            Console.Write("The scientific name for a dog is " + dog.SpeciesName + "\n");
            Console.Write("Dogs like to eat " + dog.Diet);
            Console.ReadLine();
        }
```
