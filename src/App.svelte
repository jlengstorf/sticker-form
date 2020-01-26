<style>
  * {
    box-sizing: border-box;
  }

  /*
 * see https://gist.github.com/ffoodd/000b59f431e3e64e4ce1a24d5bb36034
 */
  .sr-only {
    border: 0 !important;
    clip: rect(1px, 1px, 1px, 1px) !important;
    -webkit-clip-path: inset(50%) !important;
    clip-path: inset(50%) !important;
    height: 1px !important;
    margin: -1px !important;
    overflow: hidden !important;
    padding: 0 !important;
    position: absolute !important;
    width: 1px !important;
    white-space: nowrap !important;
  }

  main {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    font-size: 18px;
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  form {
    text-align: left;
  }

  label,
  legend {
    font-size: 1rem;
    margin: 0 0 0.125rem;
    padding: 0;
  }

  .address {
    border: 0;
    margin: 0;
    padding: 0;
    width: 100%;
  }

  .address-fields {
    border: none;
    display: grid;
    grid-template-columns: auto 130px 130px;
    grid-gap: 0.5rem;
  }

  input {
    display: block;
    background: #fff;
    border: 1px solid #bbb;
    border-radius: 0.125rem;
    font-size: 1rem;
    padding: 0.25rem;
    width: 100%;
  }

  .full-width,
  :global(.algolia-places) {
    display: block;
    grid-column: 1 / 4;
  }

  @media (min-width: 640px) {
    main {
      margin-left: auto;
      margin-right: auto;
      max-width: 90vw;
      width: 500px;
    }
  }
</style>

<main>
  <h1>Get Stickers!</h1>
  <p>
    Boop your laptop, your car, your friends, your nose — with this small-batch,
    artisinal, corgi-approved BOOP sticker you can really boop
    <em>anything</em>
  </p>
  <form name="contact" method="POST" data-netlify="true">
    <p>
      <label>
        Full Name:
        <input type="text" name="name" />
      </label>
    </p>
    <p>
      <label>
        Email Address:
        <input type="email" name="email" />
      </label>
    </p>
    <fieldset class="address">
      <legend>Where should we send your stickers?</legend>

      <div class="address-fields">
        <label class="sr-only" for="street-address">Street address</label>
        <input
          type="search"
          id="street-address"
          name="street-address"
          placeholder="Street address" />

        <label class="sr-only" for="address-line-2">
          Address line 2 (optional)
        </label>
        <input
          class="full-width"
          type="text"
          id="address-line-2"
          name="address-line-2"
          placeholder="Address line 2 (optional)" />

        <label class="sr-only" for="city">City</label>
        <input type="search" id="city" name="city" placeholder="City" />

        <label class="sr-only" for="state">State/Province</label>
        <input
          type="search"
          id="state"
          name="state"
          placeholder="State/Province" />

        <label class="sr-only" for="zip">Zip/Postal Code</label>
        <input
          type="search"
          id="zip"
          name="zip"
          placeholder="Zip/Postal Code" />

        <label class="sr-only" for="country">Country</label>
        <input
          class="full-width"
          type="search"
          id="country"
          name="country"
          placeholder="Country" />
      </div>
    </fieldset>
    <p>
      <label>
        Message:
        <textarea name="message" />
      </label>
    </p>
    <p>
      <button type="submit">Send</button>
    </p>
  </form>

  <script>
    const addressLookup = places({
      appId: "plLK27LOG37N",
      apiKey: "36ff30ffc67631d9621e96277d916f25",
      container: document.querySelector("#street-address"),
      templates: {
        value: suggestion => suggestion.name
      }
    });

    addressLookup.on("change", event => {
      console.log(event);
      document.querySelector("#state").value =
        event.suggestion.administrative || "";
      document.querySelector("#city").value = event.suggestion.city || "";
      document.querySelector("#zip").value = event.suggestion.postcode || "";
    });
  </script>
</main>
