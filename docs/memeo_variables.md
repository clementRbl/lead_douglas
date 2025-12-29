# Mémo des variables - Dataset Seattle 2016

| Nom de la colonne | Définition / Traduction (FR) |
| :--- | :--- |
| **OSEBuildingID** | Identifiant unique du bâtiment (Clé primaire). |
| **DataYear** | Année de collecte des données (ici 2016). |
| **BuildingType** | Classification générale du bâtiment (ex: Non-résidentiel, Multifamilial). |
| **PrimaryPropertyType** | Type d'usage principal déclaré (ex: Hôtel, École, Bureau). |
| **PropertyName** | Nom de la propriété ou du bâtiment. |
| **Address** | Adresse postale (rue). |
| **City** | Ville. |
| **State** | État (WA). |
| **ZipCode** | Code postal. |
| **TaxParcelIdentificationNumber** | Numéro de parcelle cadastrale. |
| **CouncilDistrictCode** | Code du district du conseil municipal. |
| **Neighborhood** | Nom du quartier. |
| **Latitude** | Latitude (Coordonnée GPS). |
| **Longitude** | Longitude (Coordonnée GPS). |
| **YearBuilt** | Année de construction du bâtiment. |
| **NumberofBuildings** | Nombre de bâtiments inclus dans la propriété. |
| **NumberofFloors** | Nombre d'étages. |
| **PropertyGFATotal** | **Surface brute totale** au sol (GFA = Gross Floor Area) en pieds carrés. |
| **PropertyGFAParking** | Surface brute dédiée au parking. |
| **PropertyGFABuilding(s)** | Surface brute dédiée aux bâtiments (hors parking). |
| **ListOfAllPropertyUseTypes** | Liste complète de tous les usages de la propriété. |
| **LargestPropertyUseType** | Usage principal (celui qui occupe la plus grande surface). |
| **LargestPropertyUseTypeGFA** | Surface occupée par l'usage principal. |
| **SecondLargestPropertyUseType** | Deuxième usage le plus important (si existant). |
| **SecondLargestPropertyUseTypeGFA** | Surface occupée par le deuxième usage. |
| **ThirdLargestPropertyUseType** | Troisième usage le plus important (si existant). |
| **ThirdLargestPropertyUseTypeGFA** | Surface occupée par le troisième usage. |
| **YearsENERGYSTARCertified** | Années où le bâtiment a obtenu la certification ENERGY STAR. |
| **ENERGYSTARScore** | Score d'efficacité énergétique (1-100). |
| **SiteEUI(kBtu/sf)** | Intensité Énergétique du Site (Conso totale / Surface). |
| **SiteEUIWN(kBtu/sf)** | Intensité Énergétique du Site **normalisée par la météo**. |
| **SourceEUI(kBtu/sf)** | Intensité Énergétique à la Source (inclut pertes de production/transport). |
| **SourceEUIWN(kBtu/sf)** | Intensité Énergétique à la Source **normalisée par la météo**. |
| **SiteEnergyUse(kBtu)** | **CIBLE POTENTIELLE 1** : Consommation totale d'énergie mesurée sur le site. |
| **SiteEnergyUseWN(kBtu)** | Consommation totale d'énergie normalisée par la météo. |
| **SteamUse(kBtu)** | Consommation spécifique de vapeur (Détail de la cible). |
| **Electricity(kWh)** | Consommation spécifique d'électricité (en kWh). |
| **Electricity(kBtu)** | Consommation spécifique d'électricité (convertie en kBtu). |
| **NaturalGas(therms)** | Consommation spécifique de gaz naturel (en therms). |
| **NaturalGas(kBtu)** | Consommation spécifique de gaz naturel (convertie en kBtu). |
| **DefaultData** | Indicateur (True/False) si des valeurs par défaut ont été utilisées. |
| **Comments** | Commentaires divers. |
| **ComplianceStatus** | Statut de conformité légale vis-à-vis de la ville. |
| **Outlier** | Indicateur si le bâtiment est considéré comme une valeur aberrante. |
| **TotalGHGEmissions** | **CIBLE POTENTIELLE 2** : Émissions totales de gaz à effet de serre (Tonnes CO2eq). |
| **GHGEmissionsIntensity** | Intensité des émissions de GES (Émissions / Surface). |