# Manual Lead Tracking

For use cases where you need manual control over lead submission (e.g., Stimulus JS, custom frameworks), the SDK exposes two functions:

## `trackLead(data)`

Submit a lead record with custom data.

```javascript
window.leadsources.trackLead({
  email: "user@example.com",
  name: "John Doe",
  phone: "555-1234",
  // ... any other fields
});
```

**When to use:**

- Custom forms built with component frameworks where form hijacking doesn't work (via `data-leadsources-form`)


**Example: Stimulus Controller**

```javascript
import { Controller } from "@hotwired/stimulus";

export default class extends Controller {
  submit(event) {
    event.preventDefault();

    // Get tracking context (visitor ID, session ID, UTM params)
    const tracking = window.leadsources.getTrackingData();

    const data = {
      email: this.element.querySelector('[name="email"]').value,
      name: this.element.querySelector('[name="name"]').value,
    };

    // Track the lead manually
    window.leadsources.trackLead(data);
  }
}
```

**HTML with Stimulus:**

```html
<div data-controller="form">
  <form>
    <input type="email" name="email" required />
    <input type="text" name="name" />
    <input type="submit" data-action="click->form#submit" value="Submit" />
  </form>
</div>
```

The SDK will automatically include UTM parameters and visitor tracking data when sending the lead record.

## `getTrackingData()`

Retrieve the current tracking data without submitting a lead.

```javascript
const trackingData = window.leadsources.getTrackingData();
```

**Returns an object containing:**

- `visitor_id` - Unique visitor identifier
- `session_id` - Current session identifier
- `utm_source` - UTM source parameter (if available)
- `utm_campaign` - UTM campaign parameter (if available)
- `utm_term` - UTM term parameter (if available)
- `utm_content` - UTM content parameter (if available)
- `channel` - Custom channel parameter (if available)
- `landing_page` - Landing page URL (if available)
- `landing_page_subfolder` - Landing page subfolder (if available)

**Example:**

```javascript
const tracking = window.leadsources.getTrackingData();

console.log(tracking);
// Output:
// {
//   visitor_id: "abc123-def456-ghi789",
//   session_id: "xyz789-uvw456-rst123",
//   utm_source: "google",
//   utm_campaign: "summer-sale",
//   utm_term: "shoes",
//   utm_content: "ad-version-a"
// }
```
