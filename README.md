# 51degrees-lite-binary


WebJar for 51Degrees Lite Binary.

To use in your Java/Play projects, do the following:

Add it as dependency to your build.sbt file:

``` libraryDependencies += "com.51degrees" % "device-detection-core" % "3.2.4.3-beta" ```

``` libraryDependencies += "org.webjars" % "51degrees-lite-binary" % "3.2-201602" ```


then create your provider like this:

```java

    private InputStream getBrowserDataStream() {
        // load resource from webjar
        return Thread.currentThread().getContextClassLoader()
                .getResourceAsStream("META-INF/resources/webjars/51degrees-lite-binary/51Degrees-Lite.dat");
    }


    public Provider createProvider() {
         try (InputStream resourceAsStream = getBrowserDataStream()) {
                byte[] array = IOUtils.toByteArray(resourceAsStream);
                return new Provider(StreamFactory.create(Arrays.copyOf(array, array.length)), 60);
            } catch (IOException e) {
                throw new RuntimeException("Failed to load 51Degrees Database from WebJar");
            } catch (Exception e) {
                throw new RuntimeException("Unhandled error when creating 51Degrees Provider", e);
            }
    }


```

More info: http://webjars.org

Upstream: http://github.com/greyflower/51degrees-lite-binary
