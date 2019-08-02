## What's this about
This repo transfers the contributions I made on the IBM's Github Enterprise account. This is needed due to a lack of functionality from Github Enterprise, which would allow to export/link contribution data to a private Github account.

## How I exported contributions?
To export the contribution data I navigated to my profile on Github Enterprise and ran the following code in developer console:

```
Array.from(document.querySelector('.js-calendar-graph-svg').querySelectorAll('rect'))
  .map(r => [r.dataset.date, +r.dataset.count])
  .filter(([date, count]) => count)
  .map(([date, count], index) => {
	let array = [];
	for (let i = 1; i <= count; i++) {
		array.push(`GIT_AUTHOR_DATE=${date}T00:00:00 GIT_COMMITTER_DATE=${date}T00:00:00 git commit --allow-empty -m "IBM Github Enterprise commit ${i}/${count} on ${date}"`)
    }
	return array.join('\n');
	})
  .join('\n')
  
```
I then copied and save this as a bash script, which I ran on this repo.
