```java
// Preload all classes in ClassGraph to avoid invoking the classloader, which would cause a deadlock under Kilt
ClassLoader cl = Thread.currentThread().getContextClassLoader();
ZipInputStream zip = new ZipInputStream(Objects.requireNonNull(MixinGenericsCoreMod.class.getResourceAsStream("/META-INF/jarjar/classgraph-4.8.189.jar")));
for (ZipEntry entry = zip.getNextEntry(); entry != null; entry = zip.getNextEntry()) {
    if (!entry.isDirectory() && entry.getName().endsWith(".class")) {
        String className = entry.getName().replace(".class", "").replace('/', '.');
        try {
            cl.loadClass(className);
        } catch (ClassNotFoundException | NoClassDefFoundError ignored) {}
    }
}
```
