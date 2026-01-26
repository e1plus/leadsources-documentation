# Leadsources SDK Functions

## `trackLead(data)`

Submit a lead record with custom data. The SDK will automatically include all lead source data and visitor journey data when sending the lead record. Used to send data to your LeadSources dashboard.

**Example:**

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


## `getTrackingData()`

Retrieve the last lead source data without submitting a lead. Used to record last click lead source data in your CRM.

**Returns an object containing:**

- `visitor_id` - Unique visitor identifier
- `session_id` - Current session identifier
- `channel` - Custom channel parameter (if available)
- `utm_source` - UTM source parameter (if available)
- `utm_campaign` - UTM campaign parameter (if available)
- `utm_term` - UTM term parameter (if available)
- `utm_content` - UTM content parameter (if available)
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
