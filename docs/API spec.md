
  * **Standardized Naming:** All ID fields will now be consistently named `recipeId`.
  * **Future-Proofing:** I've added placeholders for future features like `rating`, `reviewCount`, and `isFavorited` to the recipe response. We won't build these now, but the API will be ready for them without requiring a breaking change later.
  * **Pagination:** The search API now includes `currentPage` and `totalPages` for more robust client-side pagination logic.
  * **Data Consistency:** The ingredients now include a `unit` field (e.g., "cups", "g") for better data consistency and future functionality.

-----

### **Final PlateFlow API Design Document**

### **1. Magic Meal API** (For David, The Busy Family Organizer)

  * **Endpoint:** `/api/magic-meal`
  * **Method:** `GET`
  * **Authentication:** Requires a valid API key or session token.
  * **Success Response:** Returns a single recipe object.

### **2. Recipe Search API** (For Lena & Maya)

  * **Endpoint:** `/api/recipes/search`
  * **Method:** `POST`
  * **Request:**
      * `ingredients` (Array of Strings)
      * `filters` (Array of Strings)
      * `page` (Integer)
      * `pageSize` (Integer)
  * **Authentication:** Requires a valid API key or session token.
  * **Success Response:** Returns a paginated object with a list of matching recipes.

<!-- end list -->

```json
{
  "totalResults": 150,
  "currentPage": 1,
  "totalPages": 8,
  "recipes": [
    {
      "recipeId": "1",
      "name": "Chicken & Broccoli Pasta",
      "imageURL": "https://example.com/chicken-pasta.jpg",
      "prepTime": "20 minutes",
      "cookTime": "25 minutes",
      "matchedIngredients": 3,
      "totalIngredients": 6,
      "rating": 4.5,
      "reviewCount": 120,
      "isFavorited": false
    },
    {
      "recipeId": "2",
      "name": "Quick Chicken Stir-Fry",
      "imageURL": "https://example.com/stir-fry.jpg",
      "prepTime": "15 minutes",
      "cookTime": "10 minutes",
      "matchedIngredients": 2,
      "totalIngredients": 4,
      "rating": 4.2,
      "reviewCount": 75,
      "isFavorited": true
    }
  ]
}
```

### **3. Recipe Details API** (For All Personas)

  * **Endpoint:** `/api/recipes/{recipeId}`
  * **Method:** `GET`
  * **Authentication:** Requires a valid API key or session token.
  * **Success Response:** Returns a single JSON object with all recipe details.

<!-- end list -->

```json
{
  "recipeId": "1",
  "name": "Chicken & Broccoli Pasta",
  "imageURL": "https://example.com/chicken-pasta.jpg",
  "prepTime": "20 minutes",
  "cookTime": "25 minutes",
  "servings": 4,
  "description": "A quick and easy weeknight meal.",
  "rating": 4.5,
  "reviewCount": 120,
  "isFavorited": false,
  "ingredients": [
    {
      "name": "Pasta",
      "quantity": "1",
      "unit": "box"
    },
    {
      "name": "Chicken Breast",
      "quantity": "2",
      "unit": "pieces"
    },
    {
      "name": "Broccoli",
      "quantity": "1",
      "unit": "head"
    },
    {
      "name": "Parmesan Cheese",
      "quantity": "0.5",
      "unit": "cup"
    }
  ],
  "instructions": [
    "Cook pasta according to package directions.",
    "Sauté chicken in olive oil...",
    "Add broccoli and garlic...",
    "Combine with pasta and top with cheese."
  ],
  "nutrition": {
    "calories": "550 kcal",
    "protein": "45 g",
    "carbs": "50 g",
    "fat": "20 g"
  }
}
```
