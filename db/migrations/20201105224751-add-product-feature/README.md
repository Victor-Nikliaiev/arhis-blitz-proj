# Migration `20201105224751-add-product-feature`

This migration has been generated by Victor Nikliaiev at 11/6/2020, 12:47:51 AM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
PRAGMA foreign_keys=OFF;
CREATE TABLE "new_Product" (
    "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
    "createdAt" DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    "updatedAt" DATETIME NOT NULL,
    "name" TEXT NOT NULL,
    "description" TEXT NOT NULL,
    "userId" INTEGER,

    FOREIGN KEY ("userId") REFERENCES "User"("id") ON DELETE SET NULL ON UPDATE CASCADE
);
INSERT INTO "new_Product" ("id", "createdAt", "updatedAt", "name", "description", "userId") SELECT "id", "createdAt", "updatedAt", "name", "description", "userId" FROM "Product";
DROP TABLE "Product";
ALTER TABLE "new_Product" RENAME TO "Product";
PRAGMA foreign_key_check;
PRAGMA foreign_keys=ON
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20201105223336-add-product-feature..20201105224751-add-product-feature
--- datamodel.dml
+++ datamodel.dml
@@ -2,9 +2,9 @@
 // learn more about it in the docs: https://pris.ly/d/prisma-schema
 datasource db {
   provider = "sqlite"
-  url = "***"
+  url = "***"
 }
 generator client {
   provider = "prisma-client-js"
@@ -42,9 +42,9 @@
   id          Int      @id @default(autoincrement())
   createdAt   DateTime @default(now())
   updatedAt   DateTime @updatedAt
   name        String
-  description String?
+  description String
   user        User?    @relation(fields: [userId], references: [id])
   userId      Int?
 }
```


