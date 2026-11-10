# Get LinkedIn profile

Automatically get LinkedIn profile on linkedin.com. Get one LinkedIn profile by its public id or profile URL: name, headline, location and its geo id, current company, About text, photo, connection degree, follower count, the stable member id, and the full lists of experience, education, languages, certifications and honors, in the order the profile shows them, with LinkedIn's ids for companies and schools and dates as month and year. Reading a profile does not record a profile view; for that reason the connection count, which only the profile page shows, is null. A role's location is the text the member saved, which can be translated or misspelled. Skills are in linkedin.com/get_profile_skills and contact details in linkedin.com/get_profile_contact_info. A field is null and a list is empty when the profile does not show it. Fails with a clear message when the browser is not signed in to LinkedIn, when the profile does not exist, or when LinkedIn limits the account.

- Site: linkedin.com
- Address: `reduck/linkedin.com/get_profile`
- Updated: 2026-10-29 (v33)
- Author: Reduck AI (reduck)

## Run it

Ask an AI agent connected to Reduck over MCP (`https://mcp.reduck.ai/mcp`) to run `reduck/linkedin.com/get_profile`, or run it from a terminal:

```bash
npx @reduck-ai/cli@latest run --script reduck/linkedin.com/get_profile
```

## Input

- `publicId` (string, optional): The LinkedIn public profile id, the part after /in/ in the profile URL (for example "williamhgates"). A full profile URL is also accepted.
- `publicIds` (array, optional): Not supported since 19 Oct 2026: the run fails with a message saying so. Send one publicId per call and fan out with run_script's scripts.

## Output

- `name` (string, required): The profile owner's full name.
- `honors` (array, required)
- `education` (array, required): Every education entry, in the order the profile shows them.
- `languages` (array, required)
- `experience` (array, required): Every role, one entry per role, in the order the profile shows them. Roles at one company share its company fields.
- `profileUrl` (string, required): Canonical profile URL.
- `certifications` (array, required)
- `about` (string | null, optional): The full About text, line breaks kept. Null when the profile has no About section.
- `degree` (string | null, optional): Connection degree to the signed-in account: "1st", "2nd" or "3rd", with a trailing + for LinkedIn's 3rd-or-beyond badge. Null on your own profile or when no badge is shown.
- `geoUrn` (string | null, optional): LinkedIn's id for that location (for example "104004912"). Pass it to linkedin.com/search_people's geoUrn to find people there.
- `headline` (string | null, optional): The profile headline. Null when the profile has none.
- `location` (string | null, optional): The profile location, as LinkedIn names it. Null when the profile shows none.
- `photoUrl` (string | null, optional): The profile photo, largest size. A signed link that expires after some weeks: download the image to keep it. Null when the profile has no photo.
- `followers` (integer | null, optional): Follower count shown on the profile header. Null when the header shows none.
- `memberUrn` (string | null, optional): Stable internal member id (an ACoAA... token). Unlike publicId it never changes. Use it as connectionOf in linkedin.com/search_people.
- `connections` (string | null, optional): Connection count shown on the profile header: digits as a string, or "500+" once a member passes 500. Null when the header shows none.
- `currentCompany` (string | null, optional): The company of the first current position in the experience list. Null when no position is current.
- `currentCompanyUrn` (string | null, optional): LinkedIn's id for that company. Null when the company has no LinkedIn page.

## FAQ

### What does "Get LinkedIn profile" do?

Get one LinkedIn profile by its public id or profile URL: name, headline, location and its geo id, current company, About text, photo, connection degree, follower count, the stable member id, and the full lists of experience, education, languages, certifications and honors, in the order the profile shows them, with LinkedIn's ids for companies and schools and dates as month and year. Reading a profile does not record a profile view; for that reason the connection count, which only the profile page shows, is null. A role's location is the text the member saved, which can be translated or misspelled. Skills are in linkedin.com/get_profile_skills and contact details in linkedin.com/get_profile_contact_info. A field is null and a list is empty when the profile does not show it. Fails with a clear message when the browser is not signed in to LinkedIn, when the profile does not exist, or when LinkedIn limits the account.

### How do I automatically get LinkedIn profile on linkedin.com?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/get_profile, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/get_profile

### Is there a linkedin.com API to get LinkedIn profile?

You do not need one. "Get LinkedIn profile" drives the real linkedin.com pages in a browser, so it works whether or not linkedin.com offers an API for this.

### What information do I need to provide?

Optional: publicId, publicIds.

### What does it return?

It returns name, about, degree, geoUrn, honors, headline, location, photoUrl, education, followers, languages, memberUrn, experience, profileUrl, connections, certifications, currentCompany, currentCompanyUrn.

### Do I need to be logged in to linkedin.com?

Yes. It acts as you on linkedin.com: on your own Chrome it reuses your session, and on a Reduck-hosted browser it loads the linkedin.com cookies saved by the Reduck extension.

### Does it change anything on linkedin.com, or only read data?

It only reads. It looks things up on linkedin.com and changes nothing there.

### How do I run it?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/get_profile, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/get_profile

### Who maintains it?

It is part of Reduck's official curated catalogue.

Source: https://reduck.ai/explore/scripts/reduck/linkedin.com/get_profile
