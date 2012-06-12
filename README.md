## CTest

A simple unit test & benchmark framework for C.

```c
int main(int argc, char **argv) {
    CTEST_SUITE("Test Suite A");

    CTEST_EXPECT("Checking 1 == 1", 1 == 1);
    CTEST_EXPECT("Checking 2 == 2", 2 == 2);
    CTEST_EXPECT("Checking 2 == 3", 2 == 3);
    CTEST_EXPECT("Checking 3 == 3", 3 == 3);
    CTEST_EXPECT("Checking 9 == 9", 9 == 9);

    //Note that execution continues after CTEST_EXPECT detects a failed
    //assertion - use CTEST_ASSERT if you want to bail instead

    CTEST_SUITE("Benchmarks");

    char foobar[] = "foobar", foo[] = "foo";
    int i, times = 10000000;
    volatile int len = 0;

    CTEST_BENCH_START("strlen() 10M times");
    for (i = 0; i < times; i++) {
        len += strlen((char*)foobar);
    }
    CTEST_BENCH_END(sizeof(foobar) * times);

    CTEST_BENCH_START("memcmp() 10M times");
    for (i = 0; i < times; i++) {
        len += memcmp((void*)foo, (void*)foobar, sizeof(foo));
    }
    CTEST_BENCH_END(sizeof(foo) * 2 * times);

    CTEST_END;
}
```

This produces

![Output](http://i.imgur.com/DtNvV.png)

