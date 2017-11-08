# A nice test setup technique:

```
suite('Base Automation Tests for px-deck-selector', function(done) {
  let deckFixture;
  setup((done)=>{
    deckFixture = fixture('px-deck-selector-fixture');
    flush(()=>{
      done();
    });
  });
```
Resets `fixture` after each test run, `flush`/`done()` pair mean component has shaken itself out/stamped local DOM ready for use in your test method.
