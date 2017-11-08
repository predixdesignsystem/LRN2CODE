# WCT Tips
### A nice test setup technique:

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

### Firefox Error
If you see an error thrown by Firefox outside of the test function `document.getElementById(...).create is not a function`, try changing your test-fixture `id` from dash-case to camelCase (no idea why this works ¯\\_(ツ)_/¯ ).

### async.until/async.whilst to wait for a condition prior to assertion:
```
test('Overlay accepts style variable', function(done) {
  let div = Polymer.dom(salmonOverlay.root).querySelector('#overlay');
  async.until(
    ()=> {
      return (window.getComputedStyle(div).backgroundColor === 'rgb(250, 128, 114)');
    },
    (callback)=> {
      setTimeout(callback, 1000);
    },
    ()=> {
      assert.equal(window.getComputedStyle(div).backgroundColor, 'rgb(250, 128, 114)');
      done();
    }
  )
});
```
- First function is a test "keep repeating until `div.backgroundColor` is Salmon".
- Second is saying to wait a second until repeating the 'test'. You can also click/prod/poke the component again here to try to cause the 'test' result (e.g. click outside a dropdown to try to force it to close etc.).
- Third function states that the test has resolved (i.e. div is Salmon). Now assert the conditions you are testing and call `done()` to say that async test is finished/satisfied.

This will still timeout after 10 seconds, the standard Mocha behaviour for async tests, if the condition isn't safisfied.
