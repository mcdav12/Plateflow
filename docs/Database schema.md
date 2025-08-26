### **Final Database Schema (Firebase Optimized)**

### **1. `recipes` Collection (Root Collection)**

This will be our main collection. To ensure fast reads (which are common in a mobile app), we'll **denormalize** some data by embedding it directly within each recipe document.

  * **Document ID:** `recipeId` (string, the unique ID)

  * **Fields:**

      * `name` (string)
      * `imageURL` (string)
      * `prepTime` (string)
      * `cookTime` (string)
      * `servings` (integer)
      * `description` (string)
      * `instructions` (array of strings)
      * `rating` (float)
      * `reviewCount` (integer)
      * `nutrition` (map with fields: `calories`, `protein`, `carbs`, `fat`)
      * `filters` (map with boolean fields: `isGlutenFree`, `isVegetarian`, `isLowCarb`)
      * `ingredientList` (array of maps, embedded for quick retrieval)

    **Example `ingredientList` map:**

    ```json
    {
      "name": "Pasta",
      "quantity": 1,
      "unit": "box"
    }
    ```

    This structure ensures the front-end has all the necessary recipe data in a single, fast read, without needing to perform a slow join.

### **2. `ingredients` Collection (Root Collection)**

This collection will act as our master list of ingredients. It's used for populating the search bar and ensuring consistency.

  * **Document ID:** `ingredientId` (string, unique ID)
  * **Fields:**
      * `name` (string)

### **3. `users` Collection (Root Collection)**

This is the central location for all user-related data.

  * **Document ID:** `userId` (string, a unique ID provided by Firebase Auth)
  * **Fields:**
      * `email` (string)
      * `favoriteRecipeIds` (array of strings, for quick lookups)
      * `shoppingList` (map or sub-collection for a future feature)

### **4. `userFavorites` Collection (Root Collection)**

This collection is a more scalable approach for handling user-favorite recipes. Instead of a single array in the `users` document, this allows for a massive number of favorites without performance degradation.

  * **Document ID:** `auto-generated ID`
  * **Fields:**
      * `userId` (string)
      * `recipeId` (string)

This structure is a powerful way to handle the many-to-many relationship between users and recipes in a NoSQL environment.

### **5. `reviews` Collection (Root Collection)**

To support our future ratings and reviews feature, we'll create this collection. It's designed to be easily queried for all reviews for a specific recipe.

  * **Document ID:** `auto-generated ID`
  * **Fields:**
      * `recipeId` (string)
      * `userId` (string)
      * `rating` (integer, from 1-5)
      * `comment` (string, optional)
      * `createdAt` (timestamp)

-----

This revised database schema is highly optimized for performance and future scalability. It prevents the need for complex, multi-document joins that can be slow on mobile devices. By embracing a NoSQL approach, we've created a solid, production-ready foundation that will support all our planned features and many more we might add in the future.
