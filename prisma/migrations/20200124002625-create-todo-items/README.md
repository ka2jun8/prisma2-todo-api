# Migration `20200124002625-create-todo-items`

This migration has been generated by tatsuya at 1/24/2020, 12:26:25 AM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
CREATE TABLE "public"."TodoItem" (
    "text" text  NOT NULL DEFAULT '',
    "todo_id" SERIAL,
    "user_id" integer  NOT NULL ,
    PRIMARY KEY ("todo_id")
) 

ALTER TABLE "public"."TodoItem" ADD FOREIGN KEY ("user_id") REFERENCES "public"."User"("user_id") ON DELETE RESTRICT
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20200124002210-create-user..20200124002625-create-todo-items
--- datamodel.dml
+++ datamodel.dml
@@ -3,11 +3,19 @@
 }
 datasource db {
   provider = "postgresql"
-  url = "***"
+  url      = "postgresql://prisma:prisma@localhost:5432/prisma?schema=public"
 }
+model TodoItem {
+  text    String
+  todo_id Int    @id @default(autoincrement())
+  user_id User
+}
+
 model User {
-  user_id Int    @id @default(autoincrement())
-  name    String
+  user_id   Int        @id @default(autoincrement())
+  name      String
+  todoItems TodoItem[]
 }
+
```

