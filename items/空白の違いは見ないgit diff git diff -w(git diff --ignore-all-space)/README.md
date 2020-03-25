```
$ cat 2013-04-16-12-20-56.txt
foo
  bar
end
```
```
$ cat 2013-04-16-12-20-56.txt
baz
  foo
    bar
  end
end
```
```
$ git diff
diff --git a/2013-04-16-12-20-56.txt b/2013-04-16-12-20-56.txt
index dff13ef..ba9d9c2 100644
--- a/2013-04-16-12-20-56.txt
+++ b/2013-04-16-12-20-56.txt
@@ -1,3 +1,5 @@
-foo
-  bar
+baz
+  foo
+    bar
+  end
 end
```
```
$ git diff -w
diff --git a/2013-04-16-12-20-56.txt b/2013-04-16-12-20-56.txt
index dff13ef..ba9d9c2 100644
--- a/2013-04-16-12-20-56.txt
+++ b/2013-04-16-12-20-56.txt
@@ -1,3 +1,5 @@
+baz
   foo
     bar
   end
+end
```