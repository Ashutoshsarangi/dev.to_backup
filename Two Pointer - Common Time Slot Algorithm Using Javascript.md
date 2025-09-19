When there is a problem related to finding a common slot between 2 people.

you can use the 2-pointer technique to find out.

``` javascript

function availableDuration(slots1, slots2, d) {
    let i = 0;
    let j = 0;

    while (i < slots1.length && j < slots2.length) {
        // Finding the boundaries of the intersection, or the common slot
        const left = Math.max(slots1[i][0], slots2[j][0]);
        const right = Math.min(slots1[i][1], slots2[j][1]);
        if (right - left >= d) {
            return [left, left + d];
        }
        // Always move the pointer of the slot that ends earlier
        if (slots1[i][1] < slots2[j][1]) {
            i++;
        } else {
            j++;
        }
    }
    return [];
}

// Example usage
const slots1 = [[10, 50], [60, 120], [140, 210]];
const slots2 = [[0, 15], [60, 70]];
const d = 8;
const result = availableDuration(slots1, slots2, d);
console.log("Earliest common time slot:", result);

// Earliest common time slot: [ 60, 68 ]

```

**Reference**

For more detail information please check
https://www.geeksforgeeks.org/meeting-scheduler-for-two-persons/


