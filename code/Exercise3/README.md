# Code of your exercise

```java
class TestIfCondition {
    private double value1;
    private double value2;
    private double value3;

    public String testDirectImbrication() {
        if(value1 > 5) {
            if(value2 > 5) {
                if(value3 > 5)
                    return "All values > 5";
            }
        }
        return "There is at least one value which is not > 5";
    }

    public double testIndirectImbrication() {
        if(value1 > 5) {
            if(value2 > 5) {
                for(int i = 0; i < 5; i++) {
                    if(value3 % i == 0)
                        return 5;
                }
            }
        }
        return 0;
    }
}
```

