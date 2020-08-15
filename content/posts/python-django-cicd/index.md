+++
title = "Python, Django and GitHub CI/CD"
date = "2019-09-30"
+++


<!--more-->


* Local project setup

```python

f = sns.relplot(data=long_centered_mean_stl_ma.query("locality_name == 'Lombardia' and category=='parks'"), x="date", y="value", hue="variable",
                col="locality_name", col_wrap=2, kind="line", height=6, legend="brief", aspect=1.5, 
                  markers=True, dashes=True, facet_kws={'sharey': True, 'sharex': False})

f._legend.remove()
 
plt.subplots_adjust(#left=0.125,
                    bottom=0.1, 
                    #right=0.9, 
                    top=0.9, 
                    #wspace=0.2, 
                    hspace=0.35
                    )

# Iterate thorugh each axis
for ax in f.axes:
    ax.set(xlabel='Date', ylabel='Value') 

    handles, labels = ax.get_legend_handles_labels()
    #if handles:
    set_labels = [l.capitalize() for l in labels[1:]]
    ax.legend(
        labels=set_labels, 
        title="", 
        fancybox=True, 
        framealpha=1, 
        #shadow=True, 
        borderpad=1, 
        loc='upper left', 
        fontsize=12, 
        #frameon=False, 
        handleheight = 0.1,
      )

    # Make x and y-axis labels slightly larger
    ax.set_xlabel(ax.get_xlabel(), fontsize=16)
    ax.set_ylabel(ax.get_ylabel(), fontsize=16)

    #set ticks every week
    ax.xaxis.set_major_locator(mdates.WeekdayLocator())
    #set major ticks format
    ax.xaxis.set_major_formatter(mdates.DateFormatter('%b'))
    ax.xaxis.set_major_locator(mdates.WeekdayLocator(interval=4))

    # Make title more human-readable and larger
    if ax.get_title():
        ax.set_title("")

    # Make right ylabel more human-readable and larger 
    if ax.texts:
        # This contains the right ylabel text
        txt = ax.texts[0]
        ax.text(txt.get_unitless_position()[0], txt.get_unitless_position()[1],
                txt.get_text().split('=')[1],
                transform=ax.transAxes,
                va='center',
                fontsize='xx-large')
        # Remove the original text
        ax.texts[0].remove()
        

restriction_date = datetime.strptime('2020-02-23', '%Y-%m-%d') 
ease_restriction_date = datetime.strptime("2020-05-11", '%Y-%m-%d')

plt.axvline(restriction_date, color='k', linestyle='dashed', linewidth=1)
plt.axvline(ease_restriction_date, color='k', linestyle='dashed', linewidth=1)

plt.tick_params(axis='both',labelsize=13)

axes = plt.gca() 
axes.set_ylim([-120, 220])
```
