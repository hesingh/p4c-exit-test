# p4c-exit-test

See `p4c/testdata/p4_16_samples/exit1.p4`

I dumped FrontendLast for `exit1.p4`. I have used `p4test`.  The contents of exit1-FrontEnd_54_FrontEndLast.p4 are included below.  Note, 
since `a` is set to zeto, FrontEndLast has already removed all other statements from `if (a_0 == 32w0) {` and only retained the exit.

```
control ctrl() {
    bit<32> a_0;
    apply {
        a_0 = 32w0;
        if (a_0 == 32w0) {
            exit;
        } else {
            exit;
        }
    }
}

control noop();
package p(noop _n);
p(ctrl()) main;

```

Then, see the dump of MidEndLast for exit.p4. The contents of exit1-MidEnd_36_MidEndLast.p4 are included below.  Note, the apply{} is 
empty because the exit is removed.

```
control ctrl() {
    apply {
    }
}

control noop();
package p(noop _n);
p(ctrl()) main;
```

In summary, no issue exits with P4's `exit` when tested with p4test and latest p4c.
